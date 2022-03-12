## Gutenberg – Block Deprecation

When you start writing your own Gutenberg block, it's just a matter of time that you will write a new version of a block. You might be wandering what that means for your existing content. What will happen when you change the structure returned by the `save()` function of the block? The devs behind the Gutenberg project thought about this too. There is a mechanism that will mark the affected blocks, saying: "This block contains unexpected or invalid content." and if you have a peek in the JS console you might get a heart attack – so many errors! 😀

<figure>![00b93a42e5c04dc11af23f121c07ee2f.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1647103674609/UqjrWWFGs.png)
<figcaption>An example of the error of a deprecated block.</figcaption>
</figure>

Personally, I'd rather skip over the most painful possibility of solving this – revision of all your content where the upgraded block appears and attempting the block recovery. This leaves you with two remaining strategies how to address this:

- Create a new block with a different name and start using that.
- Define a deprecate version of the blocks and allow users to edit them using their new version.

## How does the deprecation actually work

I find it helpful to understand the order of execution what Wordpress does when the editor notices that the DOM structure produced by the new version of the blocks `save()` function doesn't match the one saved in the content. Here is what happens on the `save` side (pun intended) when editor comes across a block:

1. Read all the attributes and run the block's `save()` function and compare its result to the block's content saved on the page. Do they match? No?
1. Look for the deprecation array and iterate the attributes and `save` functions stored in these. The important gotcha here is that the array is not sequence list. The results of one deprecated version are NOT passed to the next one. Each deprecated version is evaluated independently in the order left to right as they are listed in the array. If the results of the `save` function do not satisfy the requirements, the editor moves onto the next one. If none of them can produce a satisfactory result, the *Attempt Block Recovery* overlay is displayed and errors are printed in the JS console.
1. When a fit is found, editor looks for `migrate` function. This is especially handy when the `<Innerblocks />` are involved. This function lets the developer to handle changes to the attributes and/or to create a new structure of the inner blocks then pass these to the new (current) version of the block's `save` function.
1. The values of the attributes and the template of inner blocks are passed to the new `save` function and a new content is saved when the page is updated.

## Structure of the deprecated version of a block

Every single deprecated version of the block is an object. This object has the following structure and you don't have to provide all properties.

```javascript
const v5_0_0 = {
    attributes: {
        // the structure of attributes as they were defined in the 
        // deprecated version
    },
    supports: {
        // the supports definition of the deprecated block
    },
    save({attributes, innerBlocks}) {
        // just recreate the DOM structure with content provided by 
        // the block attributes of this version of the block
    },
    migrate(attributes, innerBlocks) {
        // this function receives old attributes and inner blocks and
        // returns either attributes or an array [attributes, innerBlocks] 
        // to be used in the current block version
    },
    isEligible() {
        // If the function returns true, this deprecated version will be used.
        // Use this if the block is technically valid but you need to update 
        // its attributes
    }
}
```

### `attributes` object

The attributes of the deprecated form of the block. The amount of attributes can change quite dramatically. When we refactored our Testimonial block the new version was using a template made out of the `core/paragraph` blocks as the inner blocks of the `my-plugin/testimonial` block. The previous version of Testimonial was relying on the RichText component and storing their values in attributes `name`, `position` and `comment`. Each inner block handles its own attributes so suddenly there was no need for our block to handle these.

```json
// excerpt from the deprecated version of the block.json
// for my-plugin/testimonial
{
    // ...
    "attributes": {
        "position": {
            "type": "string",
            "source": "html",
            "selector": ".my-plugin__position"
        },
        "comment": {
            "type": "string",
            "source": "html",
            "selector": ".my-plugin__comment"
        },
        "faceOption": {
            "type": "string"
        }
    }
    // ...
}
```

The new version was left with just the attribute storing the value defining the image of the author of the testimonial.

```javascript
// excerpt from the block.json after the refactor
{
    // ...
    "attributes": {
        "faceOption": {
            "type": "string"
        }
    }
    // ...
}
```

### `supports` object

The `supports` (object) definition for the deprecated form of the block. The property `supports` is one to pay a closer attention. This is not inherited from the new version. If it is not defined it has the default values as described at [WP dev's documentation](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/). Not being aware of this can lead to a hair loss due to unexpected behaviour. My deprecation `save()` function was getting the block's class name even when I explicitly took out any dynamic code for the classes.

```javascript
// Let's call this block my-plugin/box
const deprecated = [{
    save() {
        return (
            <article className="">Lorem ipsum</article>
        );
    }
}];
```

This was producing the following code:

```html
<article class="wp-block-my-plugin-testimonial">Lorem ipsum</article>
```

Needless to say, it took me a while to arrive to such simplified use-case. Imagine how perplexed I was when I explicitly set the class to be an empty string and the block's default class name still appeared. And this was the only thing that would make this deprecation to be skipped. The solution is in disabling the blocks class name in the deprecations `supports` property.

```javascript
const deprecated = [{
    save() {
        return (
            <article>Lorem ipsum</article>
        );
    },
    supports: {
        className: false
    }
}];
```

### `save( props )` function

The save implementation of the deprecated form of the block. The editor parser uses this function to compare its result with the stored content and in case it matches it will attempt to use this deprecated version of the block. It will then look into the attributes of that version and will try to use or migrate these with the new version of the block. Other than that it works the same as the usual [block's `save()`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-edit-save/#save) function.

### `migrate( attributes, innerBlocks )` function (optional)

As I mentioned above this function will run only if the deprecated version of the `save()` function produces a valid block. You need to make sure that all the deprecated version have their own `migrate()` if it is relevant for the upgrade of the block.

In the case of our testimonial block the `migrate()` function takes the old attributes and the old inner blocks and returns values for the new version of attributes and inner blocks.

```javascript
migrate( attributes, oldInnerBlocks ) {
    const cleanedUpInnerBlocks = oldInnerBlocks.map((innerBlock) => {
        const { attributes } = innerBlock;
        // remove all the old inner block's classes and replace them with my class name
        const newAttributes = { ...attributes, className: 'my-plugin__name' };
        return {
            ...innerBlock,
            attributes: newAttributes,
        };
    });

    const newInnerBlocks = [
        ...cleanedUpInnerBlocks, // the previous version happened to use an innerBlock for the testimonial author's name
        createBlock('core/paragraph', {className: 'my-plugin__position', content: oldAttributes.position}),
        createBlock('core/paragraph', {className: 'my-plugin__comment', content: oldAttributes.comment})
    ]
    return [attributes, newInnerBlocks];
}
```

### `isEligible( attributes, innerBlocks )` function (optional)

This function will be called on every valid instance of the block. It can be useful, if you need to use a deprecation even though the result of the `save()` function matches the saved content. Think, for example, of a change in the attributes structure whilst the output returned by the `save()` functions remains the same.

Also, because it is called on every single valid (new) instance of the block, it is better to optimise for the false condition by performing a naive, inaccurate pass at inner blocks. Only when the fast pass is considered eligible is the more accurate, durable and **slower** condition evaluated.

A good and commented example of using the `isEligible()` function is the [deprecation of the core/columns block](https://github.com/WordPress/gutenberg/blob/1eaad3cbad327e9fad5d8eef93c46aa773b7080b/packages/block-library/src/columns/deprecated.js#L127).