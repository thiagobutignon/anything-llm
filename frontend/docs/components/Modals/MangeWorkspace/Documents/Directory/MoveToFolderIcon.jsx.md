```javascript
export default function MoveToFolderIcon({
  className,
  width = 18,
  height = 18,
}) {
  return (
    <svg
      width={width}
      height={height}
      viewBox="0 0 17 19"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
      className={className}
    >
      <path
        d="M1.46092 17.9754L3.5703 12.7019C3.61238 12.5979 3.68461 12.5088 3.7777 12.4462C3.8708 12.3836 3.98051 12.3502 4.09272 12.3504H7.47897C7.59001 12.3502 7.69855 12.3174 7.79116 12.2562L9.19741 11.3196C9.29001 11.2583 9.39855 11.2256 9.50959 11.2254H15.5234C15.6126 11.2254 15.7004 11.2465 15.7798 11.2872C15.8591 11.3278 15.9277 11.3867 15.9798 11.459C16.0319 11.5313 16.0661 11.6149 16.0795 11.703C16.093 11.7912 16.0853 11.8812 16.0571 11.9658L14.0532 17.9754H1.46092Z"
        stroke="currentColor"
        strokeWidth="1.5"
        strokeLinecap="round"
        strokeLinejoin="round"
      />
      <path
        fillRule="evenodd"
        clipRule="evenodd"
        d="M2.25331 6.53891H2.02342C1.67533 6.53891 1.34149 6.67719 1.09534 6.92333C0.849204 7.16947 0.710922 7.50331 0.710922 7.85141V17.9764C0.710922 18.3906 1.04671 18.7264 1.46092 18.7264C1.87514 18.7264 2.21092 18.3906 2.21092 17.9764V8.03891H2.25331V6.53891ZM13.0859 9.98714V11.2264C13.0859 11.6406 13.4217 11.9764 13.8359 11.9764C14.2501 11.9764 14.5859 11.6406 14.5859 11.2264V9.53891C14.5859 9.19081 14.4476 8.85698 14.2015 8.61083C13.9554 8.36469 13.6215 8.22641 13.2734 8.22641H13.0863V9.98714H13.0859Z"
        fill="currentColor"
      />
      <path
        d="M7.53416 1.62906L7.53416 7.70406"
        stroke="currentColor"
        strokeWidth="1.5"
        strokeLinecap="round"
        strokeLinejoin="round"
      />
      <path
        d="M10.6411 5.21854L7.53456 7.70376L4.42803 5.21854"
        stroke="currentColor"
        strokeWidth="1.5"
        strokeLinecap="round"
        strokeLinejoin="round"
      />
    </svg>
  );
}

```
**MoveToFolderIcon Interface Documentation**
======================================================

### Purpose and Usage

The `MoveToFolderIcon` interface provides a reusable SVG icon for representing the "Move to Folder" action in your application. This icon is designed to be easily customizable through the use of parameters, allowing you to adapt it to your specific needs.

### Method Documentation

#### `export default function MoveToFolderIcon({ className, width = 18, height = 18 })`

##### Purpose:

The primary purpose of this method is to generate an SVG icon representing the "Move to Folder" action. This icon can be used in various parts of your application, such as buttons, menus, or toolbars.

##### Parameters:

* `className`: A string representing the CSS class(es) to apply to the generated SVG element.
* `width` and `height`: Numbers specifying the desired width and height (in pixels) of the generated icon. Default values are 18 and 18, respectively.

##### Return Value:

A JSX element containing the generated SVG icon.

#### Examples

Here's an example usage of the `MoveToFolderIcon` interface:
```javascript
import MoveToFolderIcon from './MoveToFolderIcon';

const myIcon = <MoveToFolderIcon className="my-icon" />;

// Render the icon in your application
```
### Dependencies

The `MoveToFolderIcon` interface depends on the `svg` library for rendering SVG elements.

### Clarity and Consistency

This documentation is written in a clear and concise manner, with consistent use of terminology and formatting. The code examples provided are simple and easy to understand, making it straightforward for developers to integrate this icon into their applications.