# Extract all paths/links from an endpoint, logs into console :

[...new Set([...document.querySelectorAll("a[href]")].map(a => new URL(a.href, location.href).pathname))]
.forEach(path => console.log(path));

# Extracts all a[href] links , and outputs it into a file :

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


# Extracts all possible links under current endpoint [src] / [href] / form[action] :

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
