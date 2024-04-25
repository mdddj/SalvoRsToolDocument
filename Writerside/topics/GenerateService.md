# Generate Service

## 生成service

![img_service.png](img_service.png)

生成service会生成四个访问数据库的函数

* `add`
* `update`
* `delete`
* `find all`

...后面可能会添加更多的

> 注意需要先生成dto,否则这些struct会提示找不到

## 示例

#### 模型

```Rust
#[derive(Clone, Debug, PartialEq, DeriveEntityModel, Eq, Serialize, Deserialize)]
#[sea_orm(table_name = "post")]
pub struct Model {
    #[sea_orm(primary_key)]
    pub id: i32,
    pub title: String,
    pub content: String,
    pub category_id: i32,
}
```

#### 生成的内容

```Rust

pub async fn add_post(req: PostAddRequest) -> AppResult<PostResponse> {
    let db = DB
        .get()
        .ok_or(anyhow::anyhow!("Database connection failed."))?;
    let model = post::ActiveModel {
        id: NotSet,
        title: Set(req.title.clone()),
        content: Set(req.content.clone()),
        category_id: Set(req.category_id.clone()),
    };
    let result = Post::insert(model).exec(db).await?;
    Ok(PostResponse {
        id: result.last_insert_id,
        title: req.title,
        content: req.content,
        category_id: req.category_id,
        category: None,
    })
}

pub async fn update_post(req: PostUpdateRequest) -> AppResult<PostResponse> {
    let db = DB
        .get()
        .ok_or(anyhow::anyhow!("Database connection failed."))?;

    let find = Post::find_by_id(req.id).one(db).await?;
    if find.is_none() {
        return Err(anyhow::anyhow!("Post does not exist.").into());
    }
    let mut model: post::ActiveModel = find.unwrap().into();

    model.title = Set(req.title);
    model.content = Set(req.content);
    model.category_id = Set(req.category_id);


    let result: post::Model = model.update(db).await?;

    Ok(PostResponse {
        id: result.id,
        title: result.title,
        content: result.content,
        category_id: result.category_id,
        category: None,
    })
}

pub async fn delete_post(id: i32) -> AppResult<()> {
    let db = DB
        .get()
        .ok_or(anyhow::anyhow!("Database connection failed."))?;
    Post::delete_by_id(id).exec(db).await?;
    Ok(())
}

pub async fn post_find_all() -> AppResult<Vec<PostResponse>> {
    let db = DB
        .get()
        .ok_or(anyhow::anyhow!("Database connection failed."))?;
    let post = Post::find().all(db).await?;
    let res = post
        .into_iter()
        .map(|r| PostResponse {
            id: r.id,
            title: r.title,
            content: r.content,
            category_id: r.category_id,
            category: None,
        })
        .collect::<Vec<_>>();
    Ok(res)
}

```