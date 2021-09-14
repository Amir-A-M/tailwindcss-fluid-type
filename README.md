# 👉🏻 tailwindcss-fluid-type

![Tailwincss Fluid Type](https://github.com/davidhellmann/tailwindcss-fluid-type/raw/main/tailwindcss-fluid-type.png)

A plugin that makes the use of Fluid Type a breeze.

## 👉🏻 Installation

Install the plugin from npm:

```bash
# Using npm
npm install tailwindcss-fluid-type

# Using Yarn
yarn add tailwindcss-fluid-type
```

Then add the plugin to your tailwind.config.js file and do your settings if you're not happy with the defaults:

```js

// tailwind.config.js
module.exports = {
    theme: {
        // ...
    },
    // You have to disable the fontSize core 
    // plugins otherwise it doesn't work
    corePlugins: {
        fontSize: false,
        // ...
    },
    plugins: [
        require('tailwindcss-fluid-type'),
        // ...
    ],
};
```

## 👉🏻 Usage

Nothing changed here to the default tailwindcss configuration:

```html

<article>
    <h1 class="text-xl">Fluid type</h1>
</article>
```

## 👉🏻 Configuration

The plugin comes with a default configuration (see below) but it's possible to customize this config for your project.
As default, we use `rem` for better accessibility, but you can also use `px`.

### Default configuration

```js
// tailwind.config.js
module.exports = {
    theme: {
        // your fluid type settings
        // works only with unitless numbers
        // This numbers are the defaults settings
        fluidTypeSettings: {
            fontSizeMin: 1.125, // 1.125rem === 18px
            fontSizeMax: 1.25, // 1.25rem === 20px
            ratioMin: 1.125, // Multiplicator Min
            ratioMax: 1.2, // Multiplicator Max
            screenMin: 20, // 20rem === 320px
            screenMax: 96, // 96rem === 1536px
            unit: 'rem' // default is rem but it's also possible to use 'px'
        },
        // Creates the text-xx classes
        // This are the default settings and analog to the tailwindcss defaults
        // Each `lineHeight` is set unitless and we think that's the way to go especially in context with fluid type. 
        fluidType: {
            'xs': [-2, 1.6],
            'sm': [-1, 1.6],
            'base': [0, 1.6],
            'lg': [1, 1.6],
            'xl': [2, 1.2],
            '2xl': [3, 1.2],
            '3xl': [4, 1.2],
            '4xl': [5, 1.1],
            '5xl': [6, 1.1],
            '6xl': [7, 1.1],
            '7xl': [8, 1],
            '8xl': [9, 1],
            '9xl': [10, 1],
        },
    },
    variants: {
        fluidType: ['responsive']
    }
};
```

### Fluid type configuration without `lineHeight`

It is also possible to set just the `fontSize` without set the `lineHeight`

```js
// tailwind.config.js
module.exports = {
    theme: {
        fluidType: {
            // ...
            'base': 0,
            // ...
        }
    }
};
```

### Fluid type configuration with `lineHeight` & `letterSpacing`

And yes, you can also set the `letterSpacing` & `lineHeight` as you know from the tailwind
documentation. `letterSpacing` can be all values that you like.

```js
// tailwind.config.js
module.exports = {
    theme: {
        fluidType: {
            // ...
            'base': [0,
                {
                    lineHeight: 1.6,
                    letterSpacing: '-0.1rem',
                }
            ],
            // ...
        }
    }
};
```

## 👉🏻 Samples

### Just set the `fontSize` property

```js
// tailwind.config.js
module.exports = {
    theme: {
        fluidTypeSettings: {
            fontSizeMin: 1.125,
            fontSizeMax: 1.25,
            ratioMin: 1.125,
            ratioMax: 1.2,
            screenMin: 20,
            screenMax: 96,
            unit: 'rem'
        },
        fluidType: {
            // ...
            'base': 0,
            // ...
        }
    }
};
```

```html
<p class="text-base">The quick brown fox jumps over the lazy dogs</p>
```

```css
.text-base {
    font-size: clamp(1.125rem, calc(1.125rem + (1.25 - 1.125) * ((100vw - 20rem) / (96 - 20))), 1.25rem);
}
```

### Set the `fontSize` & `lineHeight` property

```js
// tailwind.config.js
module.exports = {
    theme: {
        fluidTypeSettings: {
            fontSizeMin: 1.125,
            fontSizeMax: 1.25,
            ratioMin: 1.125,
            ratioMax: 1.2,
            screenMin: 20,
            screenMax: 96,
            unit: 'rem'
        },
        fluidType: {
            // ...
            'base': [0, 1.6],
            // ...
        }
    }
};
```

```html
<p class="text-base">The quick brown fox jumps over the lazy dogs</p>
```

```css
.text-base {
    font-size: clamp(1.125rem, calc(1.125rem + (1.25 - 1.125) * ((100vw - 20rem) / (96 - 20))), 1.25rem);
    line-height: 1.6;
}
```

### Set the `fontSize`, `lineHeight` & `letterSpacing` property

```js
// tailwind.config.js
module.exports = {
    theme: {
        fluidTypeSettings: {
            fontSizeMin: 1.125,
            fontSizeMax: 1.25,
            ratioMin: 1.125,
            ratioMax: 1.2,
            screenMin: 20,
            screenMax: 96,
            unit: 'rem'
        },
        fluidType: {
            // ...
            'base': [0, {
                lineHeight: 1.6,
                letterSpacing: '-0.1rem',
            }],
            // ...
        }
    }
};
```

```html
<p class="text-base">The quick brown fox jumps over the lazy dogs</p>
```

```css
.text-base {
    font-size: clamp(1.125rem, calc(1.125rem + (1.25 - 1.125) * ((100vw - 20rem) / (96 - 20))), 1.25rem);
    line-height: 1.6;
    letter-spacing: -0.1rem;
}
```
