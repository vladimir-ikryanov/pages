## Welcome to GitHub Pages

[Java Style Guide](java_style_guide.md)

You can use the [editor on GitHub](https://github.com/vladimir-ikryanov/pages/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

```java
/*
 * Copyright (c) 2000-2017 TeamDev Ltd. All rights reserved.
 * TeamDev PROPRIETARY and CONFIDENTIAL.
 * Use is subject to license terms.
 */

import com.teamdev.jxbrowser.Browser;
import com.teamdev.jxbrowser.BrowserOptions;
import com.teamdev.jxbrowser.Engine;
import com.teamdev.jxbrowser.EngineOptions;
import com.teamdev.jxbrowser.Language;
import com.teamdev.jxbrowser.LoadUrlParams;
import com.teamdev.jxbrowser.ui.Size;
import java.io.IOException;

public class HelloWorld {

    public static void main(String[] args) throws IOException, InterruptedException {
        EngineOptions engineOptions = EngineOptions.newBuilder()
                .setChromiumDir("/Users/Vladimir/chromium/bin")
                .setUserDataDir("/Users/Vladimir/chromium/data")
                .setLanguage(Language.ENGLISH_US)
                .setRemoteDebuggingPort(9222)
                .setUserAgent("UseAgent")
                .build();

        BrowserOptions browserOptions = BrowserOptions.newBuilder()
                .setInitialSize(Size.newBuilder()
                        .setWidth(800)
                        .setHeight(600)
                        .build())
                .build();

        Engine engine = Engine.newInstance(engineOptions);
        Browser browser = engine.createBrowser(browserOptions);

        browser.getMainFrame().loadUrl(LoadUrlParams.newBuilder()
                .setUrl("http://teamdev.com")
                .setPostData("key=value")
                .build());
        
        browser.close();
        engine.close();
    }
}
```

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/vladimir-ikryanov/pages/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
