### Links
- practice using this [link](https://raybo.org/slides_tailwind/#/)

### setting up
- `npm init -y`
- `npm install -D @tailwindcss/jit tailwindcss postcss`
- `npx tailwind css init -p`
- edit the `package.json` file and under "scripts"-> "start" -> "`tailwindcss -o ./build/css/styles.css --watch`"
  - `o` stands for output
- edit the `tailwind.config.js` and under purge -> `./**/*.html`
  - removes all the unused tailwind css from the overall bundle, shrinking the size to bare minimum
- `npm start`
- edit the `index.html` such that the path for stylesheet is `build/css/styles.css`


#### custom builds
- in the `tailwind.config.js`
- you need to restart the server
- example of changing breakpoints
```css
module.exports = {
    theme: {
        extend: {
            screens: {
                md: '640px`
            }
        }
    }
}
```

### adding styles
- add new styles here `src/styles.css`
  - inside required
    ```
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```
  - inside part1
    ```css
    @layer base {
        h1 {
            color: salmon;
            @apply .. .. .. .. ;
        }
    }
    ```
  - inside part2
    ```css
    @layer components {
        .btn {
            @apply 
            ...
            ...
            ...;
        }
    }

- modify `package.json` file
  - `tailwindcss -i ./src/styles.css`
    - `i` stands for input
- rerun 


### Typography

#### font directives
- font families: `font-sans` `font-serif` `font-mono`
  - you can modify the font families from `theme.fontfamily`
- font size: `text-xs` `text-xm` `text-base` `text-lg` `text-xl` `text-'n'xl`
- font weight: `font-thin` `font-extralight` `font-light` `font-normal` `font-medium` `font-semibold` `font-bold` `font-extrabold` `font-black`
- font style: `italic` `not-italic`
- font smoothing: `antialiased` `subpixel-antialised`
- font variant numeric: `normal-nums` `ordinal` ...

#### text directory
- text colors: `text-[color]-[50-900]`
- text opacity: `text-opacity-[0-100]`
- text alighment: `text-left` `text-center` `text-right` `text-justify`
- text decoration: `underline` `line-through` `no-underline`
- text transform: `text-transform:`- `uppercase` `lowercase` `capitalize` `normal-case`
- text overflow: `truncate` `overflow-ellipsis` `overflow-clip`

#### list style `<ul></ul>`
- list style type: `list-none` `list-disc` `list-decimal`
- list style position: `list-style-position: `-`outside` `inside`

#### spacing typography (spacing between lines)
- line height: `leading-[3-10]` or for relative `line-height-`- `none` `tight` `snug` `normal` `relaxed` `loose`
- letter spacing: `tracking-`- `tighter` `tight` `normal` `wide` `wider` `widest`

### Object properties

- borders `border (-SID) (-AMT)` `SID: t r b l` `AMT: 0 2 4 8`
  - opacity `border-opacity-AMT` `AMT: 0 5x 100`
  - color `border-COL-STR`
  - radius `rounded-(SID)(-AMT)`
  - style `border-(STL)` STL: `none` `solid` `dashed` `dotted` `double`
- rings
  - width `ring(-AMT)`
  - opacity `ring-opacity-AMT`
  - color `ring-COL-STR`
  - offset width `ring-offset-WDT`
  - focus variants `focus:`
- divide
  - width `border(-DIR)(-AMT)` `DIR x y` `AMT 0 2 4 8 reverse`
  - opacity `divide-opacity-AMT`
  - style `divide(-STL)`
- background
  - color `bg-COL-STR`
  - opacity `bg-opacity-AMT`
  - image `bg(-none)|(-gradient-to)(-DIR)`
    - gradient color stops `(from|via|to)-COL-AMT`
  - size `bg(-TYP)` `TYP`: `auto` `cover` `contain`
  - repeat `bg(-TYP)` `TYP`: `repeat` `no-repeat` `repeat-x` `repeat-y` `repeat-round` `repeat-space`
  - position `bg(-TYP)` `TYP`: `bottom` `center` `left` `left-bottom` `left-top` `right` `right-bottom` `right-top` `top`
  - origin `bg-origin(-TYP)` `TYP`: `padding` `border` `content`
- box
  - decoration break `decoration-slice` `decoration-clone`
  - shadow `shadow(-AMT)` `AMT`: `none` `inner` `sm` `md` `lg` `xl` `2xl`
  - sizing `box-border` `box-content`


### Object Metrics
- Width and Height
  - Width `w-(SIZ)` `SIZ`: `0-100` `m/n` `auto` `px` `full` `screen` `min` `max`
  - Height `h-(SIZ)` `SIZ`: `0-100` `m/n` `auto` `px` `full` `screen`
  - Min Width `min-w-(SIZ)` `SIZ`: `0` `full` `min` `max`
  - Max Width `max-w-(SIZ)` `SIZ`: `0` `none` `xs` `sm` `md` `lg` `xl` `nxl` `full` `min` `max` `prose` `screen-sm`..
  - Min Height `max-w-(SIZ)` `SIZ`: `0` `full` `screen`
  - Max Height `max-w-(SIZ)` `SIZ`: `0` `px` `full` `screen` numbers
- Padding (inside borders)
  - `p(-DIR)(-SIZ)` `DIR`: `px` `py` `t` `r` `b` `l` `SIZ`: [0-96]
-  Margin (outside borders)
   - `(-)m(-DIR)(-SIZ)` same as padding
 - Display and Position
   - Display `block` `inline-block` `inline` `flex` `inline-flex` `flow-root` `grid` `inline-grid` `contents` `hidden` `table` `inline-table` `table-caption` `table-cell` `table-column` `table-column-group` `table-footer-group` `table-header-group` `table-row-group` `table-row` `list-item` `flow-root` `grid` `inline-grid` `contents` `hidden`
    - Position `static` `fixed` `absolute` `relative` `sticky` `(-)(SID)(-DIR)(-SIZ)` 
      - `SID`: `inset` `top` `right` `bottom` `left` 
      - `DIR` : `x` `y`
      - `SIZ` : numbers, fractions `auto` `px` `full`
- Object Floating and Containment
  - Float `float-(SID)` `DIR`: `none` `left` `right`
  - Object Fit `object-(SID)` `DIR`: `contain` `cover` `fill` `none` `scale-down`
  - Object pisition `object-(POS)` `DIR`: `left-top` `top` `right-top` `left` `center` `right` `left-bottom` `bottom` `right-bottom`
  - Other Properties
    - Z-index `z-(AMT)` `SID` `0` `10` `20` `30` `40` `50` `auto`
    - Visibility `visible` `invisible`
    - Opacity `opacity-AMT`
    - Overflow `overflow(-DIR)(-TYP)`
    - Overscroll `overscroll(-DIR)(-TYP)` `DIR`: `x` `y` `TYP`: `auto` `contain` `none`

### Layout
- Flexbox `flex(-TYP)(-DIR)` `TYP`: `row` `col` `DIR`: `reverse` 
  - flexwrap `flex-wrap` `flex-wrap-reverse` `flex-nowrap`
  - flex `flex-1` `flex-auto` `flex-initial` `flex-none`
  - flex grow `flex-grow-0` `flex-grow`
  - flex shrink `flex-shrink-0` `flex-shrink`
  - Order `order(-ORD)` `ORD` `1-12` `first` `last` `none`
- Grids
  - Grid Template Columns
    - `grid-cols-(-AMT)` `AMT`: `1-12` `none`
    - `col(-TYP)(-AMT)` `TYP`: `auto` `span` `start` `end` `AMT`: `1-12` `full`
  - Grid Template Rows
    - `grid-rows(-AMT)` `AMT`: `1-6` `none`
  - Grid Row Start/End
    - `col(-TYP)(-AMT)` `TYP` `auto` `span` `start` `end`
  - Grid Auto columns
    - `auto-cols-auto` `auto-cols-min` `auto-cols-max` `auto-cols-fr`
- Box Alignment
  - space between `space(-DIR)(-AMT)` `DIR` `x` `y` `AMT`: `0~96` `px` `reverse`
  - justify content `justify(-DIR)` `DIR`: `start` `end` `center` `between` `around` `evenly`
  - justify items `justify-items(-DIR)` `DIR`: `auto` `start` `end` `center` `stretch`
  - justify self `justify-self(-DIR)` `auto` `start` `end` `center` `stretch`
  - align items `items(-DIR)` `DIR`: `center` `start` `end` `baseline` `stretch`
  - align self `items(-DIR)` `DIR`: `center` `start` `end` `baseline` `stretch`
  - place content `place-content(-DIR)` `DIR`: `center` `start` `end` `between` `around` `evenly` `stretch`
  - place items `place-items(-DIR)` `DIR`: `auto` `start` `end` `center` `stretch`
  - place self `place-self(-DIR)` `DIR`: `auto` `start` `end` `center` `stretch`



### Animation
- Transformations
  - Transform `transform` `transform-gpu` `transform-none`
  - Rotate `(-)rotate(-DEG)` `AMT`: `0~180`
  - Scale `scale(-DIR)(-SIZ)` `DIR`: `x` `y` `SIZ`: `0~150`
  - Skew `(-)skew(-DIR)(-DEG)` `DIR`: `x` `y` `DEG`: `0` `1` `2` `3` `6` `12`
  - translate `(-)translate(-DIR)(-AMT)` `DIR`: `x` `y` `AMT`: `0~96` `px` `full`
  - transform origin `origin(-DIR)` `DIR`: `center` `top` `top-right` `right` `bottom-right` `bottom` `bottom-left` `left` `top-left`
- Transitions
  - `transition(-TYP)` `TYP`: `none` `all` `colors` `opacity` `shadow` `transform`
  - Transition Duration `duration(-TYP)` `AMT` `75` `100` `150` `200` `300` `500` `700` `1000`
  - Transition Delay `delay(-TYP)`
  - Transition Timing function `ease(-TYP)` `TYP`: `linear` `in` `out` `in-out`
- Animation
  - `animate(-TYP)` `TYP`: `none` `spin` `ping` `pulse` `bounce`
- Filter utilities
  - .....
- Blending mode utilities
  - how different layers are blended
  - isolation


### Other options
- Forms
  - Placeholder colors
  - Placeholder opacity
- Tables
  - Table Layout `table-auto` `table-fixed`
  - Border Collapse `border-collapse` `border-separate`
- SVG
  - Stroke `stroke-current`
  - Fill `fill-current`
- Screen readers `sr-only` `not-sr-only`
- Interactive
  - User select `select-TYP` `TYP`:`auto` `all` `none`
  - Cursors `cursor-TYP` `TYP`: `auto` `default` `pointer` `wait` `text` `move` `not-allowed`


## Just in time Mode
- allows you generate CSS on-demand, rather than creating a huge CSS file upfront that contains all possible combinations of classes
- so CSS is generated on the fly
- advantages
  - small files
  - arbitrary values
    - eg. `bg-[#f5e6c0]` `w-[150px]`
  - variants enabled/stackable
    - before/after variants
    - first letter/line `first-letter:` `first-line:`
    - selection variant `selection:`
    - empty variant
    - pseudo classes only `first-of-type` `last-of-type` `only-of-type` `target` `default` `intermediate` ...