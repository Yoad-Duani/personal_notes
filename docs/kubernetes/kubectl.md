```tsx
import React, { useEffect, useRef } from "react";
import { useSearchParams, useNavigate } from "react-router-dom";

const GleanSearchPage = () => {
  const containerRef = useRef<HTMLDivElement>(null);
  const [searchParams, setSearchParams] = useSearchParams();
  const navigate = useNavigate();

  useEffect(() => {
    const script = document.createElement("script");
    script.src = "https://app.glean.com/embedded-search-latest.min.js";
    script.defer = true;
    document.body.appendChild(script);

    script.onload = () => {
      if (!window.EmbeddedSearch) return;

      window.EmbeddedSearch.renderChat(containerRef.current, {
        chatId: searchParams.get("chatId") ?? "",
        onChat: (chatId: string) => setSearchParams({ chatId }),
        onSearch: (query: string) =>
          navigate({
            pathname: "/search",
            search: new URLSearchParams({ query }).toString(),
          }),
      });
    };

    return () => {
      document.body.removeChild(script);
    };
  }, [searchParams, setSearchParams, navigate]);

  return (
    <div
      ref={containerRef}
      style={{
        height: "100%",
        width: "100%",
        position: "relative",
        display: "flex",
        flexDirection: "column",
        alignItems: "center",
        justifyContent: "center",
        padding: "24px",
      }}
    />
  );
};

export default GleanSearchPage;
```
