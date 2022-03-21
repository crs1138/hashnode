## Gutenberg cheatsheet – Block's `supports` property

Gutenberg's documentation has come a long way and it's getting better and better. However, now and then I find myself missing a quick overview of the properties. Thus the idea of a cheatsheet…

Here's a short overview of the individual properties of the `supports` object for details refer to [developer's documentation](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/):

- [`anchor`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#anchor) - boolean: `false`.  
  It doesn't work with dynamic blocks (yet).
- [`align`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#align) - boolean/array: `false`  
  No default alignment is assigned. If you need to set a default value, declare the `align` attribute with its default.
- [`alignWide`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#alignwide) - boolean: `false`  
  Disable [wide alignment](https://developer.wordpress.org/block-editor/how-to-guides/themes/theme-support/#wide-alignment) for a single block.
- [`className`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#classname) - boolean: `true`  
  **By default, the class `.wp-block-your-block-name` is added to the root element of your saved markup.**
- [`color`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#color) - Object: `null`  
  This value signals that a block supports some of the properties related to color. When it does, the block editor will show UI controls for the user to set their values.
- [`customClassName`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#customclassname) - boolean: `true`  
  Controls whether the field for custom class name is displayed in the panel inspector.
- [`defaultStylePicker`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#defaultstylepicker) - boolean: `true`  
  When the style picker is shown, the user can set a default style for a block type based on the block’s currently active style.
- [`html`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#html) - boolean: `true`  
  By default, a block’s markup can be edited individually.
- [`inserter`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#inserter) - boolean: `true`  
  To hide a block so it can only be inserted programmatically, set the `inserter: false`.
- [`multiple`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#multiple) - boolean: `true`  
  If you want a block to be inserted into each post only once.
- [`reusable`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#reusable) - boolean: `true`  
  You can prevent a block from being converted into a reusable block.
- [`spacing`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#spacing) - Object: `null`  
  You can enable some of the CSS style properties related to spacing. Good for margin and padding overrides, if [the theme declares support](https://developer.wordpress.org/block-editor/how-to-guides/themes/theme-support/#cover-block-padding).
  Subproperties:
  - `margin` - boolean/array: `false`
  - `padding` - boolean/array: `false`
- [`typography`](https://developer.wordpress.org/block-editor/reference-guides/block-api/block-supports/#typography) - Object: `null`
  When enabled, the block editor will show a typography UI.
  Subproperties:
  - fontSize - boolean: `false`
  - lineHeight - boolean: `false`


The values of the attributes added by the `supports` object will be added to the object returned from the `useBlockProps()` hook.

Within the `Edit` function:
```javascript
function Edit() {
	const blockProps = useBlockProps();
	return (
		<div {...blockProps}>Lorem ipsum</div>
	);
}
```

`Save` function:
```javascript
function Save() {
	const blockProps = useBlockProps.save();
	return (
		<div {...blockProps}>Lorem ipsum</div>
	);
}
```

For dynamic and server-side rendered blocks these extra attributes can get rendered in the `render_callback` in PHP using the function `get_block_wrapper_attributes()`. It returns a string containing all the generated properties and needs to get output in the opening tag of the wrapping block element.

```php
function render_block() {
	$wrapper_attributes = get_block_wrapper_attributes();
	return sprintf(
		'<div %1$s>%2$s</div>',
		$wrapper_attributes,
		'Lorem ipsum'
	);
}
```

---
Cover image by [Emma Plunkett – The Missing Peace](https://www.emmaplunkett.art/artwork/missing-peace/)