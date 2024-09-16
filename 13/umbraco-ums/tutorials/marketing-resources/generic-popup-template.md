Enjoy this easy-to-use popup template and start boosting your marketing activities right away!  
No help is needed from a developer, everyone can set this one up. Apply some personalization to make the popup even more relevant for your audience. [Read this blog](https://www.umarketingsuite.com/blog/a-personalized-popup-in-5-minutes/ "Setting up a personalized popup within 5 minutes with uMarketingSuite") if you want to set up a personalized popup within uMarketingSuite.

Please make sure that you've installed [the clientside script](/analytics/clientside-events-and-additional-javascript-files/additional-measurements-with-our-ums-analytics-scripts/) of the uMarketingSuite on your website to make sure you can use the full functionality!  
  
*The resources needed for this popup are shared below the screenshot. ![uMarketingSuite Popup example]()*

## JavaScript

This popup won't affect the styling of your existing page or website. To be able to apply the popup we need some JavaScript to insert the popup HTML in your existing content.  In addition, we would like visitors to have the possibility to close the popup. This coding is also added.

Now simply copy and paste the javascript below into uMarketingSuite.

    var popupTitle = "Popups do convert!"; // The title of your popup
    var popupText = "The average conversion rate of a popup is 3.09%So, if you have 1000 visitors on a daily basis, each month 927 visitors will convert through this popup."; // The text of your popup
    var popupbuttonText = "I want this!"; // The button text
    var popupButtonLink = "https://www.umarketingsuite.com/"; // The button link
    var popupButtonClose = "X"; // The close button text
    var popupName = "Popup1"; // Must be unique, used as analytics event and cookiename
    const useCookie = true; // Set this to true to use a cookie to hide the popup for visitors that closed the popup or clicked on the button.
    const cookieExpireDays = 30; // After how many days do you want this popup to re appear?

    // Do no change anything below this line //
    const CookieService = {
          setCookie(name, value, days) {
            let expires = '';
      
            if (days) {
              const date = new Date();
              date.setTime(date.getTime() + days * 24 * 60 * 60 * 1000);
              expires = '; expires=' + date.toUTCString();
            }
      
            document.cookie = name + '=' + (value || '') + expires + ';';
          },
      
          getCookie(name) {
            const cookies = document.cookie.split(';');
      
            for (const cookie of cookies) {
              if (cookie.indexOf(name + '=') > -1) {
                return cookie.split('=')[1];
              }
            }
      
            return null;
          },
        };
        
    function checkCookie() {if (useCookie) {	CookieService.setCookie(`ums` + popupName + `Shown`,true,cookieExpireDays);
            }};
        
    function sendEvent(eventvalue) {ums("send", "event", "Popup", eventvalue, popupName);
        };
        
    function hideModel() {const message = document.querySelector('.u-alert-message');message.remove();
        sendEvent('Closed');checkCookie();
        };
    
    function registerClick() {sendEvent('Clicked');checkCookie();
        };
    
    var popupContent = `<div class="u-alert-message absolute"><article class="u-alert-content"><strong>` + popupTitle + `</strong><p>` + popupText + `</p><div class="u-alert-button-container"><a href="` + popupButtonLink + `" class="u-alert-button secondary" onclick="registerClick();">` + popupbuttonText + `</a></div></article><button id="js-close-alert" class="u-alert-close u-alert-button" onclick="hideModel();">` + popupButtonClose + `</button></div>`
    
    const hasCookie = CookieService.getCookie(`ums` + popupName + `Shown`);if (!hasCookie) {	document.body.insertAdjacentHTML('beforeend', popupContent);};

## CSS

Now that we have our popup in place we would like to make it look a bit fancier. Copy and paste this CSS into uMarketingSuite and your popup is ready to go.

You can change the font, colors and other properties at the top of the CSS code.

Don't be scared to play around with other properties. If things go wrong, this copy is here to reset your styling ;-)

        :root {
    
    /* 
    Change these values to customize the looks of your popup
    If you need a color picker go to https://www.w3schools.com/colors/colors_picker.asp
    Click on 'Or Use HTML5' to use the colorpicker (the pipette icon)
    */
    
    --c-text: #000000;			/* Text color */
    --c-font-text: system-ui, sans-serif;	/* Text font */
    --c-size-text: 16px;			/* Text size */
    --c-lh-text: 28px;			/* Text line spacing */
    --c-title: #3444b2;			/* Title color */
    --c-font-title: system-ui, sans-serif;	/* Title font */
    --c-background: #ffffff; 		/* Popup background color */
    --c-radius: 20px; 			/* Popup border radius */
    --c-btn-text: #ffffff; 			/* Button text color */
    --c-btn-background: #11bc9b; 		/* Button background color */
    --c-btn-radius: 5px; 			/* Button border radius */
    --c-close-text: #cccccc; 		/* Close button text color */
    --c-close-background: #f2f2f2; 		/* Close button background color eaeaea*/
    --c-close-radius: 5px; 			/* Close button border radius */
    }

    /* Do no change anything below this line */
    .u-alert-message {
    position: relative;
    background: var(--c-background);
    border-radius: var(--c-radius);
    padding: 50px 50px 35px;
    max-width: min(100%, 520px);
    box-sizing: border-box;
    font-family: var(--c-font-text);
    color: var(--c-text);
    line-height: var(--c-lh-text);
    opacity: 0;
    animation: showAnim 1s cubic-bezier(0.4, 0.2, 0.2, 1) forwards;
    transition: all 1s;
    font-size: var(--c-size-text);
    box-shadow: 2px 2px 30px rgb(0 0 0 / 25%);
    }
    
    .u-alert-message.absolute {
    --sides: 60px;
    position: fixed;
    z-index: 1000;
    bottom: var(--sides);
    right: var(--sides);
    }
    
    .u-alert-content strong {
    font-size: 1.2em;
    max-width: 90%;
    display: inline-block;
    font-family: var(--c-font-title);
    color: var(--c-title);
    }
    
    .u-alert-content p {
    margin: 10px 0 0 0;
    }
    
    .u-alert-button-container {
    margin-top: 20px;
    display: flex;
    justify-content: flex-end;
    flex-wrap: wrap;
    margin-bottom: -5px;
    }
    
    .u-alert-button-container > * {
    margin-bottom: 5px;
    }
    
    .u-alert-button-container > *:not(:last-child) {
    margin-right: 5px;
    }
    
    .u-alert-button {
    appearance: none;
    border: 0;
    background: var(--c-primary-surface);
    color: var(--c-primary-contrast);
    padding: 8px 20px;
    border-radius: var(--c-btn-radius);
    font-family: inherit;
    font-size: 1em;
    font-weight: 600;
    text-decoration: none;
    transition: filter 0.2s ease;
    cursor: pointer;
    }
    
    .u-alert-button:hover,
    .u-alert-button:focus {
    filter: brightness(1.1);
    }
    
    .u-alert-button.secondary {
    background: var(--c-btn-background);
    color: var(--c-btn-text);
    }
    
    .u-alert-close {
    position: absolute;
    top: 10px;
    right: 25px;
    padding: 5px 10px;
    font-size: 0.8em;
    background: var(--c-close-background);
    color: var(--c-close-text);
    border-radius: var(--c-close-radius);
    }
    
    @media (max-width: 48em) {
    .u-alert-message.absolute {
    max-width: 100%;
    width: 100%;
    border-bottom-left-radius: 0;
    border-bottom-right-radius: 0;
    --sides: 0;
    }
    .u-alert-button:not(.u-alert-close) {
    width: 100%;
    text-align: center;
    }
    }
    
    @keyframes showAnim {
    0% {
    opacity: 0;
    transform: scale(0.5);
    }
    100% {
    opacity: 1;
    transform: scale(1);
    }
    }

## Questions or ideas?

Do you have improvements or requests for other templates that you would like to use? Feel free to reach out to [contact@umarketingsuite.com](mailto:contact@umarketingsuite.com?subject=Marketing%20Resources%20suggestion "Reach out to uMarketingSuite with your suggestion"). We would love to hear from you!