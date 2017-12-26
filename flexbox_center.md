Centering elements using flexbox is very simple and is one of the easiest way to center stuff. It is very reliable and easy. It feel it is easier then margin:0 auto technique. So lets get into it.

## HTML for testing

```html
<div class="flex-container">
    <div class="flex-item">
    </div>
</div>
```

Only this much is requied for testing

## CSS

```css
.flex-container {
  display: flex;
  align-items: center; /* This will vertically center them */
  justify-content: center; /* This will horizontally center them*/
  width: 300px;
  height: 300px;
  background: blue;
}

.flex-item {
  height: 50%;
  width: 50%;
  background: red;
}
```

## Result

<div class="flex-container">
    <div class="flex-item">
    </div>
</div>

## Conclusion

Flexbox is really powerful tool for web designers and it is now 97% supported worldwide with even even more support if you prefix it. Start using flexbox today
