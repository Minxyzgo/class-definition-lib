# ClassDefinition
### example
`> main.js`
```js
const $ = require("classDefinition/classDefinition")
const customImageButtonClass = $.defineClass("example.CustomImageButton", ImageButton,
  {
    public: {
      build: null,
      'super(Drawable,ImageButton.ImageButtonStyle) constructor$1': function(drawable, style, build) {
        this.build = build
      },
      'super() constructor$0': function () {
        //code...  
      },
      constructor() {
        //code...  
      },
      
      newMethod() {}
    },
    override: {
      draw() {
        this.super$draw()
      },
      'callafter() updateImage': function () {
        let build = this.build
        if (build != null && build.building != null) {
          let drawable = build.progress == -1 ? build.building.drawable(): Icon.hammer
          let image = this.getImage()
          let color = image.color;
          let style = this.getStyle()

          if (this.isDisabled && style.imageDisabledColor != null)
            color = style.imageDisabledColor;
          else if (this.isPressed() && style.imageDownColor != null)
            color = style.imageDownColor;
          else if (this.isChecked() && style.imageCheckedColor != null)
            color = style.imageCheckedColor;
          else if (this.isOver() && style.imageOverColor != null)
            color = style.imageOverColor;
          else if (style.imageUpColor != null)
            color = style.imageUpColor;
          image.setDrawable(drawable);
          image.setColor(color);
        } else this.super$updateImage()
      }
    }
  }
)

let button = new customImageButtonClass(Icon.add, new ImageButton.ImageButtonStyle(), {building: null})
//...
```

### usage
Use `defineClass(className, superclass, interfaces..., body)` Note that the superclass is initally Object.

Struct
```js
$.defineClass("example", {
    public: {
        //...    
    },
    protected: {
        //...    
    },
    private: {
        //...  
    },
    override: {
        //...    
    }
})
```
You can define your new fields and methods in `public`, `protected` and `private` block.

`override` block is used for overriding superclass methods. And you cannot define any new fields or methods here.

### identifiers
There are some special identifiers in the lib, which can fix some annoying problems.

- callafter
> usage: `callafter(args...)`
> If you override some methods invoked in the constructor of the superclass, rhino will throw a `NullPointerException`. So `callafter` is used for marking a method that will be invoked later with the given parameters.

- super
> usage: `super(args...)`
> Use it on `constructor`.
