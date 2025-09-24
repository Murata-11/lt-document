# DTO（Data Transfar Object）の理解を深める

## はじめに

これまで色んな場面で目にしたり使っていた DTO（Data Transfar Object）。しかし、人に説明できるほどその概念を詳しく知りませんでした。今回はそんな DTO について理解していきたいと思います。

## 目次

1. DTO とは？
2. 実はデザインパターンだった
3. ドメイン駆動設計における DTO について
4. まとめ

## 1. DTO とは？

Wiki によると、

> Data Transfer Object（DTO）はデザインパターンの一種で、アプリケーションソフトウェアのサブシステム間でデータを転送するのに使う。

出典: https://ja.wikipedia.org/wiki/Data_Transfer_Object

主にシステム間でデータを転送するために用いられるそうです。

では実際どのように使用されるのかプログラムを見ながら確認します。

```golang
// 入力（リクエスト）: フロントエンド → バックエンド
type CreateUserRequestDTO struct {
	Name     string `json:"name"`
	Email    string `json:"email"`
	Password string `json:"password"`
}

// 出力（レスポンス）: バックエンド → フロントエンド
type UserResponseDTO struct {
	ID    int    `json:"id"`
	Name  string `json:"name"`
	Email string `json:"email"`
}
```

この例では、フロントエンドとバックエンド間のリクエストとレスポンスを受け取る構造体として DTO を定義しています。
このようにデータを安全に変換（JSON ↔ 構造体）するために DTO を用いています。

また、DTO は以下の特徴があります。

1. ビジネスロジックを持たない
   - DTO の役割は「データをまとめて運ぶ」ことに専念します
2. 安全性が高まる
   - 転送可能なデータが限定されます
   - 型の安全性を高めることができます

次に、デザインパターンである DTO がどのような問題を解決するために考えられたのか見ていきましょう。

## 2. 実はデザインパターンだった

ソフトウェア開発において、データを正確に表現するためにデータクラスを使用することで表現する方法が一般的です。
しかし、

https://martinfowler.com/eaaCatalog/dataTransferObject.html
