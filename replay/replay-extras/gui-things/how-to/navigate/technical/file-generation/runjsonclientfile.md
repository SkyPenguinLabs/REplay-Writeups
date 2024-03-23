---
cover: ../../../../../../../.gitbook/assets/image.avif
coverY: 0
---

# RunJsonClientFile

{% hint style="info" %}
This function fetches from a remote source where the URL is just a&#x20;
{% endhint %}

```cpp
void RunJsonClientDLLJSONFile() {
// Information for temporary github imports and resolutions for API usage
    std::filesystem::path  OP = CURRENT_MOD_PATH / "client.dll.jso" ;
    std::string curlCommand = "curl -sS " + std::string(R) + " -o " + OP.string();
    system(curlCommand.c_str());
}
```
