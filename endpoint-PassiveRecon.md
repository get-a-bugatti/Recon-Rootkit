### Extract all paths/links from an endpoint, logs into console :
```
[...new Set([...document.querySelectorAll("a[href]")].map(a => new URL(a.href, location.href).pathname))]
.forEach(path => console.log(path));
```

### Extracts all a[href] links , and outputs it into a file :
```
(() => {
    const paths = [...new Set([...document.querySelectorAll("a[href]")].map(a => new URL(a.href, location.href).pathname))];
    
    const blob = new Blob([paths.join("\n")], { type: "text/plain" });
    const a = document.createElement("a");
    a.href = URL.createObjectURL(blob);
    
    const domain = location.hostname.replace(/^www\./, ""); 
    a.download = `${domain}.txt`;
    
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
})();
```

### Extracts all possible links under current endpoint [src] / [href] / form[action] :
```
const base = location.origin;

const getLocalPath = url => {
  try {
    const u = new URL(url, base);
    return u.origin === base ? u.pathname : null;
  } catch {
    return null;
  }
};

const selectors = [
  '[href]',
  '[src]',
  'form[action]',
  'script',
];

const elements = [...document.querySelectorAll(selectors.join(','))];

const paths = [...new Set(
  elements
    .map(el => el.getAttribute('href') || el.getAttribute('src') || el.getAttribute('action'))
    .map(getLocalPath)
    .filter(p => p)
)];

paths.forEach(p => console.log(p));

```