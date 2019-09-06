# playcanvas-gltf
![Alt text](/images/duck.jpg?raw=true "Title")

## loadGltf
gltf는 텍스쳐들이 참조하기 때문에 (glb는 포함압축이진) 그냥 아래와 같이 로드하면 텍스쳐들이 적용됩니다.
하지만, 텍스쳐가 없는 gltf 에 texture mapping을 하려면 좀 다르게 해야합니다.
examples/index.html를 확인하세요
스크린샷의 오리는 default로 mapping된것이고, 바퀴는 custom mapping입니다.
### Example
```javascript
app.assets.loadFromUrl('assets/monkey/monkey.gltf', 'json', function (err, asset) {
    var json = asset.resource;
    var gltf = JSON.parse(json);
    loadGltf(gltf, app.graphicsDevice, function (err, res) {
        // Wrap the model as an asset and add to the asset registry
        var asset = new pc.Asset('gltf', 'model', {
            url: ''
        });
        asset.resource = res.model;
        asset.loaded = true;
        app.assets.add(asset);

        // Add the loaded scene to the hierarchy
        var gltf = new pc.Entity('gltf');
        gltf.addComponent('model', {
            asset: asset
        });
        app.root.addChild(gltf);
    }, {
        basePath: 'assets/monkey/'
    });
});
```
