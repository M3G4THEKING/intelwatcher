# Intel Watcher

A script that allows you to scrape the Ingress Intel Map and use that information to fill a database or update Stops/Gyms that have missing info.

### Credits
- [ClarkyKent](https://github.com/ClarkyKent/ingress_scraper) who made the original Scraper
- [The Ingress API](https://github.com/lc4t/ingress-api) this is based on

## Setup
### Database
Intel Watcher uses PMSFs database structure. If you have PMSF set up, just put its DB name in your config to also have Portals shown on your Map. Else, you can run `mysql your_db_name < ingress_portals.sql` to create a new table.

### Cookies
Intel Watcher needs to be able to log into the Intel Map in order to get Portal info. It does that with the login cookie.

#### Notes
- Use a burner Account to the Cookie (!!) **Scraper Accounts have been banned before**
- The cookie runs out after 14 days. Intel Watcher can send Discord Webhooks when that happens, so you can manually get a new one. To re-new your cookie, follow below steps but begin with 2.

### Get a cookie
1. Create an Ingress account using the Ingress Prime app on your phone
2. Open a new incognito window in your browser
2. Log into your burner account [here](https://intel.ingress.com/intel) with the same Email
3. Zooming into your area *may* improve results. (not confirmed)
4. Press F12 and go to the Network tab, refresh the site (F5), then select `intel` in left coulumn and your window should look something like the Screenshot below. (Chrome)

![csrftoken-same-cookie](https://i.imgur.com/y7KFNI0.png)

5. Now copy everything after `cookie:` (the content highlighted in the red box) and paste it into `cookie.txt`

### BBOX
To set up an area to scrape, go to [bboxfinder.com](http://bboxfinder.com), and select your desired area using the rectangle tool. Now copy the String after `Box` in the bottom field.

Note that you can use multiple bboxes in your config by seperating them with `;`. e.g. `-0.527344,5.441022,27.246094,20.138470;2.245674,48.795557,2.484970,48.912572`

![BBOX params](https://i.imgur.com/QKROPSU.jpg)

### Running the script
Now proceed as usual: `pip3 install -r requirements.txt`, fill in the config and you're done.
- `python3 intel_watcher.py` to scrape the area
- `python3 intel_watcher.py -u` to update Gyms and Stops with missing title andhoto
