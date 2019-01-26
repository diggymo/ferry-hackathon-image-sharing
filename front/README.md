# Hackathon共有用プロジェクト！！

## 仕様

APIサーバーの仕様

### request

GET http://ferry-sunflower.ga/api/v1/qr/{QRID}

### response

```json
[
    {
        image: "xxxx_yyyy_zzzzz_hrejigoragha.jpg", // 画像URL,
        created_at: "2018-10-10 11:22:33", // 撮影日時。できればほしい笑
        spot: {
            id: 4,
            name: "別府地獄巡り",
            description: "人気の温泉観光地。おどろおどろしい地獄の名が付けられ、柵で囲われたさまざまな湯だまりがある。動物たちも飼育されている。"
        }
    },
    {
        image: "xxxx_yyyy_zzzzz_hrejigoragha.jpg", // 画像URL,
        created_at: "2018-10-11 22:33:44", // 撮影日時。できればほしい笑
        spot: {
            id: 1,
            name: "由布岳",
            description: "由布岳は、大分県由布市にある標高1,583mの活火山。山体が阿蘇くじゅう国立公園に指定されている。"
        }
    }   
]

```

## 環境構築

```
cd front
```

### Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn run serve
```

### Compiles and minifies for production
```
yarn run build
```

### Lints and fixes files
```
yarn run lint
```
