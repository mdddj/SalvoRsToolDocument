# Antd: Struct生成Form表单


可以选中struct名称,鼠标单击右键,会出现一个`生成antd表单`的菜单选项

![img_antd_form.png](img_antd_form.png)

它会生成一个form表单提交的react代码

## 示例

## struct模型
```Javascript
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
```

## 生成的代码


需要自己去实现添加和修改两个操作

```Javascript
type Prop = {
  trigger?: JSX.Element | undefined,
  initValues?: PropInitValue | undefined
}
interface PostAddRequest {
	title: string,
	content: string,
	category_id: number,
}

const AddOrUpdateForm: React.FC<Prop> = (props) => {
  let isUpdate = props.initValues !== undefined
  //提交数据
  const onFinish = async (values: PropInitValue) => {
    if(isUpdate) {
      // Todo! 修改
    }else{
      // ToDo! 新增
    }
    return true
  }
  return (
    <ModalForm<PropInitValue> trigger={props.trigger} initialValues={props.initValues} onFinish={onFinish}>
      		<ProFormText name='title' label='标题' rules={[
					{ message: '请输入标题', required: true}
			]}
 		/>
		<ProFormText name='content' label='正文内容' rules={[
					{ message: '请输入正文内容', required: true}
			]}
 		/>
		<ProFormDigit name='category_id' label='分类ID' rules={[
					{ message: '请输入分类ID', required: true}
			]}
 		/>

    </ModalForm>
  );
};
export {AddOrUpdateForm}

```