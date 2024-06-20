# IMDb Watchlist Random Movie Picker
A browser bookmark which, when on your IMDb watchlist page, will scroll to a random point on the page, and highlight a film to watch. If you're not happy with the choice, just click it again to get another recommendation.

![image](preview.webp)

## Installation
Just get the link from **[this webpage](https://lc.mt/imdb-bookmarklet)**, and drag it to your bookmarks bar.

(_Github doesn't support embedding javascript links on their site._)

## Source code
It's just simple js. Here is the source code:

```javascript
javascript:(function(){var e;function t(){var e=document.getElementsByClassName("ipc-metadata-list-summary-item");if(0===e.length)return;let t=e[Math.floor(Math.random()*e.length)];t.style.cssText="background:#F9FABE;box-shadow:0px 0px 20px #FF0;padding:10px;margin:10px;border-radius:10px;transition:all 0.5s;",t.scrollIntoView({behavior:"smooth",block:"center"}),setTimeout(()=>t.style.cssText="",3e3)}e||((e=document.createElement("div")).style.cssText="position:fixed;top:50%;left:50%;transform:translate(-50%, -50%);padding:20px;background:rgba(0,0,0,0.8);color:white;z-index:1000;font-size:20px;text-align:center;box-shadow:0 4px 6px rgba(0,0,0,0.1);",e.innerText="Loading all films...",document.body.appendChild(e)),function a(){var n=parseInt(document.querySelector('div[data-testid="list-page-mc-total-items"]').innerText.match(/\d+/)[0]);document.getElementsByClassName("ipc-metadata-list-summary-item").length<n?(document.querySelector('div[data-testid="list-page-mc-list-content"]').scrollIntoView({behavior:"smooth",block:"end"}),setTimeout(a,750)):(e&&e.parentNode&&(e.parentNode.removeChild(e),e=null),setTimeout(t,500))}()})();
```

Here it is unminified:

```javascript
javascript:(function() {
    var notificationBox;  // Global reference for the notification box

    function createNotificationBox() {
        if (!notificationBox) {  // Only create if it does not already exist
            notificationBox = document.createElement('div');
            notificationBox.style.cssText = 'position:fixed;top:50%;left:50%;transform:translate(-50%, -50%);padding:20px;background:rgba(0,0,0,0.8);color:white;z-index:1000;font-size:20px;text-align:center;box-shadow:0 4px 6px rgba(0,0,0,0.1);';
            notificationBox.innerText = 'Loading all films...';
            document.body.appendChild(notificationBox);
        }
    }

    function removeNotificationBox() {
        if (notificationBox && notificationBox.parentNode) {
            notificationBox.parentNode.removeChild(notificationBox);  // More reliable removal
            notificationBox = null;  // Clear the reference to avoid future conflicts
        }
    }

    function scrollToRandomFilm() {
        var films = document.getElementsByClassName('ipc-metadata-list-summary-item');
        if (films.length === 0) return;
        const selectedFilm = films[Math.floor(Math.random() * films.length)];
        selectedFilm.style.cssText = 'background:#F9FABE;box-shadow:0px 0px 20px #FF0;padding:10px;margin:10px;border-radius:10px;transition:all 0.5s;';
        selectedFilm.scrollIntoView({ behavior: 'smooth', block: 'center' });
        setTimeout(() => selectedFilm.style.cssText = '', 3000);
    }

    function checkAllFilmsLoaded() {
        var totalItemsText = document.querySelector('div[data-testid="list-page-mc-total-items"]').innerText;
        var totalItems = parseInt(totalItemsText.match(/\d+/)[0]); // Extract number from the text
        var loadedItems = document.getElementsByClassName('ipc-metadata-list-summary-item').length;

        if (loadedItems < totalItems) {
            var listContentDiv = document.querySelector('div[data-testid="list-page-mc-list-content"]');
            listContentDiv.scrollIntoView({ behavior: 'smooth', block: 'end' }); // Scroll to the end of the list
            setTimeout(checkAllFilmsLoaded, 750); // Recheck after a delay
        } else {
            removeNotificationBox();
            setTimeout(scrollToRandomFilm, 500);
        }
    }

    createNotificationBox();
    checkAllFilmsLoaded();
})();
```
