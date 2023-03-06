# Optimizing Application Loading

This page is used to discuss how to optimize the loading time of applications. It holds key terms and discusses key concepts at length.

## Vocab and Terminology

- Compression
- Minification
- Static Assets
- Throttling
- First Contentful Paint
- Time To Interactive

Optimizing Application Loading Research

1. Optimizing Page Load Tutorial

[Chrome DevTools - Chrome Developers](https://developers.google.com/web/tools/chrome-devtools/speed/get-started#top_of_page)

2. Calculating download speeds
    1. 1 bit = 1 or 0
    2. 1 Byte = 8 Bits
        1. A single letter or character with UTF-8 (e.g. “A”, “$”) = up to 4 Bytes, usually 1 Byte or 8 bits
        2. An integer (e.g. 2000, 1, or -300) = 2 or 4 Bytes (depending on the number range)
    3. Kilobyte (KB): 1000 bytes = 1 KB (Kilo means one thousand)
        1. A short email (text only) = 5 KB
        2. A five-page paper = 10 KB
        3. A small animated GIF = 834 KB
    4. Megabyte (MB): 1000 KB = 1 MB (Mega means one million)
        1. The average size of a webpage = 2 MB
        2. A 3-minute long MP3 file = 3 MB
        3. A standard CD-ROM = 700 MB
    5. Gigabyte (GB): 1000 MB = 1 GB (Giga means one billion)
        1. 256 MP3 files = 1 GB
        2. 600 high-resolution images = 2GB
        3. A standard DVD = 4.38 GB
    6. Terabyte (TB): 1000 GB = 1 TB (Tera means one trillion)
        1. 1,000 copies of the Encyclopedia Britannica = 1 TB
        2. 400,000 songs = 2 TB
        3. 900,000,000 photos = 3 TB
    7. So how do you calculate download speeds?
        1. You take file size, and divide by download speed. But they need to be the same unit to measure!
        2. Internet speeds are usually measured in BITS not BYTES. Bits are the smallest unit of measure, and 8 bits make up 1 byte.
        3. So when you sign up for “1 GIG” internet, you’re not getting 1 GigaBYTE, you’re actually getting 1 GigaBIT! Scammy and confusing? Sure, but now you know better than most!
    8. Let’s calculate the download time for an animated gif with 3G internet:
        1. A 3G internet device might get around 750 kiloBITS per second (not kilobytes) download. Remember there are 8 bits for every 1 byte.
        2. So a single animated GIF we figured is 834 kiloBYTES works out to be 6,672 kilobits (834 X 8 = 6,672 kilobits) would take about 9 seconds to load with 3G internet!
3. The Cost of JavaScript 

    <iframe width="548" height="308" src="https://www.youtube.com/embed/63I-mEuSvGA" title="The Cost Of JavaScript - Addy Osmani - Fluent 2018" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

4. Critical Rendering Path
    1. The Critical Rendering Path is the sequence of steps the browser goes through to convert the HTML, CSS, and JavaScript into pixels on the screen. Optimizing the critical render path improves render performance.The critical rendering path includes the [Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) (DOM) and the [CSS Object Model](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model) (CSSOM), render tree and layout.
    2. Optimizing the critical rendering path improves the time to first render. Understanding and optimizing the critical rendering path is important to ensure reflows and repaints can happen at 60 frames per second, to ensure performant user interactions, and to avoid [jank](https://developer.mozilla.org/en-US/docs/Glossary/Jank).