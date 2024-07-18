# Generate Router

## Generate router

![img_router.png](img_router.png)

Generating a router will generate the corresponding API interface for addition, deletion, modification and query by default.

> Note that you need to generate dto first, otherwise these structs will prompt that they cannot be found.

## example

#### data model
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

#### generated content

```Rust


#[endpoint(tags("博客"))]
pub async fn post_add_post(new_post: JsonBody<PostAddRequest>) -> AppWriter<PostResponse> {
    let result = post::add_post(new_post.0).await;
    AppWriter(result)
}

#[endpoint(tags("博客"),parameters(
    ("id",description="博客ID")
),)]
pub async fn put_update_post(req: &mut Request) -> AppResult<AppWriter<PostResponse>> {
    let req: PostUpdateRequest = req.extract().await?;
    let result = post::update_post(req).await;
    Ok(AppWriter(result))
}

#[endpoint(tags("博客"))]
pub async fn delete_post(id: PathParam<i32>) -> AppWriter<()> {
    let result = post::delete_post(id.0).await;
    AppWriter(result)
}


#[endpoint(tags("博客"))]
pub async fn get_post_all() -> AppWriter<Vec<PostResponse>> {
    let result = post::post_find_all().await;
    AppWriter(result)
}

```

