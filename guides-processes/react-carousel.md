![d5hqar2idkoefh6fjtpu](https://user-images.githubusercontent.com/96712943/213082489-0fdd88f8-60c4-499f-8339-a9952716f9fa.png)

# React Carousel

## Carousel creation using the React Carousel Package

- Installation
  - ```npm i react react-dom @trendyol-js/react-carousel```
- Importing
  - ```import { Carousel } from '@treandyol-js/react-carousel'```
- Building a carousel is easy using the carousel package. Let's build out a simple carousel below
```javascript
import React from 'react'
import ReactDom from 'react-dom';
import { Carousel } from '@trendyol-js/react=carousel';
import { Item } from './yourItem';

const PictureCarousel () => {
	<Carousel>
		<Item />
		<Item />
		<Item />
		<Item />
	</Carousel>
}
```
- Carousel Information
  - The syntax for creating a carousel component is relatively simple and it mirrors other components. ```<Carousel />```. Props are passed down as they always are in components and here is a list of some of the props you can pass down.
    
| Name | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| Children | Node[] | true | [] | Child items that will be wrapped by carousel |
| Show | Number | false | 1 | Number of items to show at per slide |
| Slide | Number | false | 1 | Number of how many items to slide |
| infinite | boolean | false | true | scrolling infinity |
| transition | number | false | 0.5 | same as css transition property's second value |
| swiping | boolean | false | false | enable swiping/dragging with mouse/touch events |
| swipeOn | number | false | 1 | percentage of item width that slides when user drag count exceeds |
| responsive | boolean | false | false | enables the feature that adjusts items width according to screen size dynamically |
| className | string | false | "" | same as react's className property |
| useArrowKeys | boolean | false | false | enables sliding when press arrow keys |
| a11y | Array | false | {} | accessibility attributes |
| dynamic | Boolean | false | false | if items are stateful, specify this option as true. Also give unique key to each item (like id) |
| rightArrow | ReactElement | false | null | custom right arrow component |
| leftArrow | ReactElement | false | null | custom left arrow component |

- Scrolling Carousel
  - Scrollable carousel like google's web component ```g-scrolling-carousel```
  - ```<ScrollingCarousel />```

| Name | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| children | Node[] | true | [] | Child items that will be wrapped by carousel |
| className | string | false | "” | same as react’s className property |

- Infinite Carousel
  - Carousel is infinite at default
```javascript
<Carousel show={3.5} slide={2} transition={0.5}>
	<Highlight color="#f27a1a">We love Trendyol orange</Highlight>
  <Highlight color="#d53f8c">This is our github</Highlight>
  <Highlight color="#16be48">We love Trendyol green</Highlight>
  <Highlight color="#3f51b5">This is our website</Highlight>
</Carousel>
```

- Swipeable Carousel
    - Carousel you can swipe items with your mouse or touch screen
```javascript
<Carousel show={3.5} slide={3} swiping={true}>
    <Highlight color="#2d66c3">We love Web 🌐</Highlight>
    <Highlight color="#f44336">We love Developers 👩🏻‍</Highlight>
    <a target="_blank" href="https://github.com/trendyol/">
        <Highlight color="#d53f8c">This is our github</Highlight>
    </a>
    <a target="_blank" href="https://trendyol.com/">
        <Highlight color="#f27a1a">This is our website</Highlight>
    </a>
    ...
</Carousel>
```

- Scrolling Carousel
    - Scroll, drag or click arrows to slide carousel
```javascript
<ScrollingCarousel>
  <Item />
  <Item />
  <Item />
  <Item />
</ScrollingCarousel>
```