# GenerateDTO

## 生成tdo模型

如果你用的是sea orm 数据生成的Entity,可以快速生成dto实体

> 注意需要获取到数据库表名才可以,根据这个来识别的`#[sea_orm(table_name = "table_name")]`


生成的命名方式: 携带下划线的表名会自动命名为驼峰的方式

`tag_post`->`TagPost`

![1.gif](1.gif)

## 示例

#### 数据模型
```Javascript

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
```Javascript

///添加博客模型
#[derive(Deserialize, Debug, Validate, ToSchema, Default)]
pub struct PostAddRequest {
    ///标题
    #[salvo(schema(example = "test"), parameter(description = "标题"))]
    pub title: String,
    ///正文内容
    #[salvo(schema(example = "test content"))]
    pub content: String,
    ///分类ID
    #[salvo(schema(example = 1))]
    pub category_id: i32,
}

///修改博客模型
#[derive(Debug, Deserialize, Extractible, ToSchema, Default)]
#[salvo(extract(default_source(from = "body", parse = "json")))]
pub struct PostUpdateRequest {
    ///主键ID
    #[salvo(extract(source(from = "param")))]
    pub id: i32,
    ///标题
    pub title: String,
    ///正文内容
    pub content: String,
    ///分类ID
    pub category_id: i32,
}

///返回博客模型
#[derive(Debug, Serialize, ToSchema, Default)]
pub struct PostResponse {
    ///主键ID
    pub id: i32,
    ///标题
    pub title: String,
    ///正文内容
    pub content: String,
    ///分类ID
    pub category_id: i32,
    ///分类模型
    pub category: Option<CategoryResponse>,
}

```