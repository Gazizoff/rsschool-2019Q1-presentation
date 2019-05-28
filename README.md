# rsschool-2019Q1-presentation
Hello, my name is Konstantin and today I would like to tell you about the strategy of downloading fonts to your web site.  
Custom web fonts are used everywhere around the world, but many  sites load them improperly.  
This causes a lot of problems for page loading like performance issues, slow loading time,  
blocked rendering and swapped fonts during navigation.  
Let’s try to answer the question: How to load web fonts to avoid performance issues and speed up page loading?  
`Click slide`  
 There are just four steps to consider when loading a custom web font:  
•	Use the correct font format `click`  
•	Preload fonts `click`  
•	Use the correct font-face declaration `click`  
•	Avoid invisible text during font loading. `click`  
Let’s break down these points one at a time. `click`  
**Use the correct font format**  `click`
There are many font formats that can be used on the web, but only two formats are really needed  
if you don’t have to support Internet Explorer (IE) 8 or lower: Web Open Font Format (WOFF) and woff2.  
These are the only two file types you should use because they are compressed in the gzip format by default (so they are very small),  
are optimized for the web, and are fully supported by IE 9+ and all other browsers.  
**Preload fonts**  `click`  
When using custom fonts you should tell the browser to preload them using the appropriate rel="" tag and attributes, 
let's look on example:`click`  
Note that the use of crossorigin here is important; without this attribute, the preloaded font is ignored by the browser, 
and a new fetch takes place. This is because fonts are expected to be fetched anonymously by the browser, 
and the preload request is only made anonymous by using the this attribute.
In the above example, the rel="preload" as="font" attributes will ask the browser to start downloading the required 
resource as soon as possible. They also tell the browser that this is a font, so it can appropriately  
prioritise it in its resource queue. Using the preload hints will have a dramatic impact on web font  
performance and initial page load. Browsers that support preload and prefetch hints will start  
downloading web fonts as soon as they have seen the hint in the HTML file and no longer need to wait for the CSS.  
You can instead use the rel="prefetch" attribute to tell the browser to prepare the download of  
the resources that may be required later during page load or user actions so it will assign a low priority to those resources.  
CAUTION:  
If you’re using a CDN like Google Fonts, be sure that the font files you’re preloading match the ones in the CSS.  
Fonts can also be regularly updated, and if you’re preloading an old version while using the CSS for a newer one,  
you may end up downloading two versions of the same font and wasting your users’ bandwidth.  
Consider using <link rel="preconnect"> instead for easier maintenance.  
**Correct font-face declaration**`click`  
Declaring a font-face family is very simple but we must take care with certain things when we do it.  
Here a correct example declaring a custom font family: slide  
As you can see we use only optimised fonts (Web Open Font Format  and WOFF2) and in addition to font  
properties such as style, weight, and stretch we tell the browser to load only the required glyphs range (from U+000 to U+5FF).  
This enables us to split a large Unicode font into smaller subsets and only download the glyphs required to render  
the text on a particular page, but this property doesn’t prevent browsers to download the entire font.  
There are also two more things to note, the local() function and the font declaration order.  
The local() function allows users to use their local copy of the font if present  
(e.g. think about the Roboto fonts that are pre-installed on Android) instead of downloading it.  
The font declaration order is also important because the browser will start fetching the resources by following the declaration order.  
If it supports the woff2 format it will download the font, or if it doesn’t recognize the resource format it will proceed  
to the next one, and so on.  
If you really want to use EOT and TTF fonts make sure to add them at the end of the src declaration.  
**Avoid invisible text during font loading**`click`  
Fonts are often large files that take a while to load even when gzipped. To deal with this,  
some browsers hide text until the font loads (the “flash of invisible text”).  
You can avoid the “flash” and show content to users immediately using a system font initially, then replacing it.  
In the previous @font-face example you’ll notice the font-display declaration.  
The swap value tells the browser that text using this font should be displayed immediately using a system font.  
Once the custom font is ready, the system font is swapped out.  
If a browser does not support font-display it continues to follow its default behaviour for loading fonts.  
Browser default behaviours if a font is not ready:  
Edge uses a system font until the custom font is ready, then swaps out fonts.  
Chrome will hide text for up to 3 seconds. If text is still not ready, it will use a system font until the custom font is ready.  
Firefox will hide text for up to 3 seconds. If text is still not ready, it will use a system font until the custom font is ready.  
Safari hides text until the custom font is ready.  
**Conclusion**`click`  
In conclusion I would like to say that we must account for situations where the connection speed  is not optimal  
or when people don’t have time to wait several seconds while your app/site is being completely loaded and navigable.  
Such improvements, especially for large projects, are mandatory for improving overall user experience, and they really don’t  
require a lot of effort.  

Thanks for your attention.  
