# IMDB Watchlist Random Picker
A browser bookmark which, when on your IMDb watchlist, will scroll to a random point on the page, and highlight a film to watch. If you're not happy with the choice, just click it again to get another recommendation.

![image](https://user-images.githubusercontent.com/19354076/216614121-42473764-aefb-498d-9910-f390baacc12a.png)


## Installation
Just get the link from **[this webpage](https://lc.mt/imdb-bookmarklet)**, and drag it to your bookmarks bar.

Github doesn't support embedding javascript links on their site.

## Source code
It's just simple js. Here is the source code:

    javascript:(()=>{for(var e=document.getElementsByClassName("load-more");e[0];)e[0].scrollIntoView(),e[0].click(),e=document.getElementsByClassName("load-more");var o=document.getElementsByClassName("lister-item featureFilm"),t=Math.floor(Math.random()*o.length),l=o[t].style.backgroundColor;o[t].style.backgroundColor="#F9FABE",o[t].style.boxShadow="0px 0px 22px #FF0",o[t].style.transition="all 2s",o[t].scrollIntoView({behavior:"smooth"}),setTimeout(()=>{o[t].style.backgroundColor=l,o[t].style.boxShadow=""},3e3)})();

Here it is unminified:

	javascript:(function(){	
		var load_more_button = document.getElementsByClassName('load-more');
		while(load_more_button[0]){
			load_more_button[0].scrollIntoView();
			load_more_button[0].click();
			load_more_button = document.getElementsByClassName('load-more');
		}
		var films = document.getElementsByClassName('lister-item featureFilm');
		const random_i = Math.floor(Math.random() * films.length);
		const old_colour = films[random_i].style.backgroundColor;
		films[random_i].style.backgroundColor = "#F9FABE";
		films[random_i].style.boxShadow = "0px 0px 22px #FF0";
		films[random_i].style.transition = "all 2s";
		films[random_i].scrollIntoView({behavior: 'smooth'});
		setTimeout(() => {
			films[random_i].style.backgroundColor = old_colour;
			films[random_i].style.boxShadow = "";
		}, 2000);
	})();
