# IMDb Watchlist Random Movie Picker
A browser bookmark which, when on your IMDb watchlist page, will scroll to a random point on the page, and highlight a film to watch. If you're not happy with the choice, just click it again to get another recommendation.

![image](preview.webp)

## Installation
Just get the link from **[this webpage](https://lc.mt/imdb-bookmarklet)**, and drag it to your bookmarks bar.

(_Github doesn't support embedding javascript links on their site._)

## Source code
It's just simple js. Here is the source code:

```javascript
javascript:(function(){function t(){var t=document.getElementsByClassName("ipc-metadata-list-summary-item");if(0===t.length)return;let e=Math.floor(Math.random()*t.length),o=t[e];o.style.backgroundColor="#F9FABE",o.style.boxShadow="0px 0px 20px #FF0",o.style.padding="10px",o.style.margin="10px",o.style.borderRadius="10px",o.style.transition="all 0.5s",o.scrollIntoView({behavior:"smooth",block:"center"}),setTimeout(()=>{o.style.backgroundColor="",o.style.boxShadow="",o.style.padding="",o.style.margin="",o.style.borderRadius=""},3e3)}document.querySelector('div[data-testid="ip_ref"]')?function e(){var o,l=document.querySelector('div[data-testid="ip_ref"]');l?(!function t(){if(!document.getElementById("loadingNotification")){var e=document.createElement("div");e.id="loadingNotification",e.style.position="fixed",e.style.top="50%",e.style.left="50%",e.style.transform="translate(-50%, -50%)",e.style.padding="20px",e.style.backgroundColor="rgba(0,0,0,0.8)",e.style.color="white",e.style.borderRadius="10px",e.style.zIndex="1000",e.style.fontSize="20px",e.style.textAlign="center",e.style.boxShadow="0 4px 6px rgba(0,0,0,0.1)",e.innerText="Just scrolling to the bottom to load all the films before picking a random one :-)",document.body.appendChild(e)}}(),l.scrollIntoView({behavior:"smooth",block:"end"}),setTimeout(e,1000)):((o=document.getElementById("loadingNotification"))&&o.remove(),setTimeout(t,500))}():t()})();
```

Here it is unminified:

```javascript
javascript:(function() {
    function createNotificationBox() {
        var existingBox = document.getElementById('loadingNotification');
        if (!existingBox) {
            var notificationBox = document.createElement('div');
            notificationBox.id = 'loadingNotification';
            notificationBox.style.position = 'fixed';
            notificationBox.style.top = '50%';
            notificationBox.style.left = '50%';
            notificationBox.style.transform = 'translate(-50%, -50%)';
            notificationBox.style.padding = '20px';
            notificationBox.style.backgroundColor = 'rgba(0,0,0,0.8)';
            notificationBox.style.color = 'white';
            notificationBox.style.borderRadius = '10px';
            notificationBox.style.zIndex = '1000';
            notificationBox.style.fontSize = '20px';
            notificationBox.style.textAlign = 'center';
            notificationBox.style.boxShadow = '0 4px 6px rgba(0,0,0,0.1)';
            notificationBox.innerText = 'Just scrolling to the bottom to load all the films before picking a random one :-)';
            document.body.appendChild(notificationBox);
        }
    }

    function removeNotificationBox() {
        var notificationBox = document.getElementById('loadingNotification');
        if (notificationBox) {
            notificationBox.remove();
        }
    }

    function scrollToRandomFilm() {
        var films = document.getElementsByClassName('ipc-metadata-list-summary-item');
        if (films.length === 0) return;
        const randomIndex = Math.floor(Math.random() * films.length);
        const selectedFilm = films[randomIndex];

        // Highlight the selected film
        selectedFilm.style.backgroundColor = "#F9FABE"; // Light yellow background
        selectedFilm.style.boxShadow = "0px 0px 20px #FF0"; // Glowing shadow
        selectedFilm.style.padding = "10px";
        selectedFilm.style.margin = "10px";
        selectedFilm.style.borderRadius = "10px";
        selectedFilm.style.transition = "all 0.5s"; // Smooth transition for styles

        selectedFilm.scrollIntoView({ behavior: 'smooth', block: 'center' });
        // Remove highlight after some time
        setTimeout(() => {
            selectedFilm.style.backgroundColor = ""; // Reset background color
            selectedFilm.style.boxShadow = ""; // Reset box shadow
            selectedFilm.style.padding = "";
            selectedFilm.style.margin = "";
            selectedFilm.style.borderRadius = "";
        }, 3000); // Highlight duration
    }

    function handleScrolling() {
        var loadMoreDiv = document.querySelector('div[data-testid="ip_ref"]');
        if (loadMoreDiv) {
            createNotificationBox();
            loadMoreDiv.scrollIntoView({ behavior: 'smooth', block: 'end' });
            setTimeout(handleScrolling, 750);
        } else {
            removeNotificationBox();
            setTimeout(scrollToRandomFilm, 1000); // Wait a bit before scrolling to film
        }
    }

    // Initialise scrolling or directly scroll to film
    var loadMoreDivExists = document.querySelector('div[data-testid="ip_ref"]');
    if (loadMoreDivExists) {
        handleScrolling();
    } else {
        scrollToRandomFilm();
    }
})();
```
