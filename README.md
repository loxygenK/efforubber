# efforubber

**+=== EXPERIMENTAL ／ 初期開発中 ===**

リポジトリに配置されたファイルを収集し、作成したリポジトリの情報を集約するGitHub Actionです。

## what this

特定のユーザのリポジトリを走査して、`.efforubber`を収集し、一つのJSONファイルにまとめるCIです。

JSONファイルはFirebaseにAPIを投げると取得することができます。エンドポイントのURLはまだわかんないです。

### `.efforubber`

以下の形式で記述されるyamlファイルです。

```yaml
efforubber:
	name: musical-typer
	description: |-
		曲に合わせて歌詞をタイピングするゲームです。
		設計はしっかりと考えなければならないことが
		よく伝わるコードを書いてしまいました。
	genre: ゲーム
	author: ...
	url: ...
```

`...`は自動置き換えを使用することを表す記号です。

自動置き換えを使用すると以下のように置換されます:

| 自動置き換えするプロパティ | 内容               |
| -------------------------- | ------------------ |
| `name`                     | リポジトリの名前   |
| `description`              | リポジトリの説明   |
| `genre`                    | `null`             |
| `author`                   | リポジトリの作成者 |
| `url`                      | リポジトリへのURL  |

`...`を書かずにプロパティの記載そのものを省略することもできます。全て省略した場合は以下のようになります。

```yaml
efforubber:
```

### JSONデータ

ここはまだ明確には決まっていないです。以下のようなものを返すつもりです。

`https://domain/api/v1/loxygenK`

```json
{
  "status": "success",
  "acquired_username": "loxygenK",
  "repos": {
    "musical_typer": {
      "name": "musical-typer",
      "description": "曲に合わせて歌詞をタイピングするゲームです。設計はしっかりと考えなければならないことがよく伝わるコードを書いてしまいました。",
      "genre": "ゲーム",
      "url": "https://github.com/loxygenK/musical_typer",
      "author": "loxygenK",
      "tags": [
        "Python",
        "Pygame"
      ]
    },
    "trailegger": {
      "name": "trailegger",
      "description": "OSUのキーボード版みたいなの作ろうとしたら無理だったやつです。",
      "genre": "ゲーム",
      "url": "https://github.com/loxygenK/trailegger",
      "tags": []
    }
  }
}
```

