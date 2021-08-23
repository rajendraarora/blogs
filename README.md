[Research blog](https://blogs.rajendraarora.com)
-------------------------------------------------


![instruction](https://i.stack.imgur.com/mbLTw.png)


# Troubleshooting

Not having the includes directory means you are using Jekyll themes.

Look in _config.yml the line that starts with "theme: " , like for example "theme: minima" and note that name.

Now you need to copy that theme includes directory into your Jekyll site directory so you can edit it. Locate that theme with: bundle show <theme name> for example:

 `bundle show minima`
It will return something like: `/var/lib/gems/minima`

Copy the _includes directory to your Jekyll dir.

 `cp -r /var/lib/gems/minima/_includes .`

Open ./_includes/footer.html and locate the repeating title. 


## Production build

```
JEKYLL_ENV=production bundle exec jekyll build --destination ../site
```