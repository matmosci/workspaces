# Workspaces

Yet another flowchart app

## Demo Content

```json
[
    {
        "id": "1",
        "title": "The first node",
        "elements": [
        {
            "type": "text",
            "data": "Lorem ipsum dolor sit amet consectetur adipisicing elit. Facere minus repellendus deserunt corporis!"
        }
        ],
        "position": {
            "x": 296,
            "y": 41
        }
    },
    {
        "id": "2",
        "title": "The second node",
        "elements": [
        {
            "type": "image",
            "data": "download.jpeg"
        }
        ],
        "position": {
            "x": 76,
            "y": 191
        }
    }
]
```

##### Add demo content to browser's localStorage

```js
localStorage.setItem('nodes','[{"id":"1","title":"The first node","elements":[{"type":"text","data":"Lorem ipsum dolor sit amet consectetur adipisicing elit. Facere minus repellendus deserunt corporis!"}],"position":{"x":74,"y":41}},{"id":"2","title":"The second node","elements":[{"type":"image","data":"download.jpeg"}],"position":{"x":76,"y":191}}]')
```