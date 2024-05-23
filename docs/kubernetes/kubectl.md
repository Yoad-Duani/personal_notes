# Kubectl

```tsx
// plugins/glean-search/src/components/EmbeddedSearchGallery.tsx
import React, { useEffect, useRef, useState } from "react";
import { useSelector } from "react-redux";
import injectScript from "./injectScript"; // Add this helper function
import styles from "./EmbeddedSearchGalleryStyles"; // Add this styles file

const lightTheme = {
  borderLight: "#eaebed",
  hover: "#f5fcfc",
  primaryHighlight: "#087d76",
  primaryHover: "#1ca99e",
  selected: "#e8fcfb",
  textPrimary: "#1b2126",
  textSecondary: "#71747d",
  visited: "#7400be",
};

interface EmbeddedSearchProps {
  authToken?: string;
}

const GleanSearch = ({ authToken }: EmbeddedSearchProps) => {
  const [query, setQuery] = useState("");
  const elementRef = useRef<HTMLDivElement>(null);
  const basePath = useSelector((state: any) => state.auth.basePath);

  useEffect(() => {
    if (!elementRef.current) return;

    (window as any).EmbeddedSearch.renderSearchBox(elementRef.current, {
      authToken,
      backend: basePath,
      onSearch: setQuery,
      query,
      searchBoxCustomizations: {
        borderRadius: 10,
        boxShadow: "none",
        horizontalMargin: 0,
        placeholderText: "Search for anything (Beta)",
        verticalMargin: 0,
      },
      theme: { light: lightTheme },
    });
  }, [authToken, basePath, query, setQuery]);

  return <div ref={elementRef} style={styles.searchBox} />;
};

const GleanSearchResultsPage = ({ authToken }: EmbeddedSearchProps) => {
  const [query, setQuery] = useState("");
  const elementRef = useRef<HTMLDivElement>(null);
  const basePath = useSelector((state: any) => state.auth.basePath);

  useEffect(() => {
    if (!elementRef.current) return;

    (window as any).EmbeddedSearch.renderSearchResults(elementRef.current, {
      authToken,
      backend: basePath,
      onSearch: setQuery,
      query,
      theme: { light: lightTheme },
    });
  }, [authToken, basePath, query, setQuery]);

  return <div ref={elementRef} style={styles.serp} />;
};

const fetchAuthToken = async (): Promise<string> => {
  // Replace this with your actual logic to fetch the auth token
  return "your-auth-token";
};

const EmbeddedSearchGallery = () => {
  const [authToken, setAuthToken] = useState<string | undefined>();
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    (async () => {
      const token = await fetchAuthToken();
      setAuthToken(token);
    })();
    injectScript({
      id: "embedded_search",
      src: "/embedded-search-latest.min.js",
    }).then(() => setIsLoading(false));
  }, []);

  if (isLoading) return null;

  return (
    <div style={styles.container}>
      <GleanSearch authToken={authToken} />
      <GleanSearchResultsPage authToken={authToken} />
    </div>
  );
};

export default EmbeddedSearchGallery;
```

</br>
</br>
</br>

```tsx
// plugins/glean-search/src/components/injectScript.ts
const injectScript = ({ id, src }: { id: string; src: string }) => {
  return new Promise((resolve, reject) => {
    const existingScript = document.getElementById(id);
    if (existingScript) {
      resolve(existingScript);
      return;
    }

    const script = document.createElement("script");
    script.src = src;
    script.id = id;
    script.onload = () => resolve(script);
    script.onerror = () => reject(new Error(`Failed to load script: ${src}`));
    document.body.appendChild(script);
  });
};

export default injectScript;
```

</br>
</br>
</br>

```tsx
// plugins/glean-search/src/components/useLazyThunk.ts
import { useCallback } from "react";
import { useDispatch } from "react-redux";

export const useLazyThunk = (thunks: any, thunkName: string) => {
  const dispatch = useDispatch();
  return useCallback(
    (...args: any) => dispatch(thunks[thunkName](...args)),
    [dispatch, thunks, thunkName]
  );
};
```

</br>
</br>
</br>

```tsx
// plugins/glean-search/src/components/selectors.ts
import { useSelector } from "react-redux";

export const selectBasePath = (state: any) => state.auth.basePath;
```
