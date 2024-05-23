```css
/* GleanSearchComponent.css */
#autocomplete-container {
  display: block;
  position: relative;
  height: 60px;
  width: 500px;
}

#native-search-box {
  margin-right: 10px;
}

#search-results {
  width: 100%;
  height: 400px;
}

.header {
  font-size: 20px;
  margin: 30px 0 10px;
}

.row {
  display: flex;
}

#chat-container {
  height: 800px;
  width: 750px;
  max-width: 100%;
  margin-bottom: 48px;
}
```

```tsx
// GleanSearchComponent.tsx
import React, { useEffect } from "react";
import "./GleanSearchComponent.css";

const GleanSearchComponent: React.FC = () => {
  useEffect(() => {
    // Inject the script
    const script = document.createElement("script");
    script.src = "https://app.glean.com/embedded-search-latest.min.js";
    script.defer = true;
    document.body.appendChild(script);

    script.onload = () => {
      const attach = (query: string | undefined = undefined) => {
        (window as any).EmbeddedSearch.attach(
          document.getElementById("search-box"),
          {
            domainsToOpenInCurrentTab: ["github.com"],
            onSearch: (query: string) => {
              const latestSearch = document.getElementById("latest-search");
              if (latestSearch) {
                latestSearch.innerText = query;
              }
            },
            query,
          }
        );
      };

      attach();
    };

    return () => {
      document.body.removeChild(script);
    };
  }, []);

  return (
    <div>
      <div className='row'>
        <input id='search-box' placeholder='search' type='text' />
      </div>
      <div id='search-results' />
    </div>
  );
};

export default GleanSearchComponent;
```
