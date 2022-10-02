# danielhayes.tech

This is a personal blog that I am doing as a small project to learn development using Hugo.

Static app is hosted via render.com.


# Why did I do this?

I got tired of using WordPress and read an article about another person attempting to deploy a static web app with Hugo.

I originally set out to deploy this in Azure via a static web app, however due to cost savings I chose to use Render.com

# Technology/Stacks Used

|   Technology  | Why   |
| ------------- |-------|
| Hugo          | Hugo go BRRRRRR   |
| Render        | It's free?        |

# Note to self
The theme is using an npm package called webpack, when changes are made to the style.css file you have to run:

```
npm run build
```

Style may not update because it is cached, turn off cache in dev tools for instant results. 