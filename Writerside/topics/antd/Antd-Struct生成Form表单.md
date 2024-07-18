# Struct generate Form


You can select the struct name, right-click the mouse, and a menu option of `Generate antd form` will appear.

![img_antd_form.png](img_antd_form.png)

It will generate a react code for form submission

## Example

## struct model

```Rust
#[derive(Deserialize, Debug, Validate, ToSchema, Default)]
pub struct PostAddRequest {

    #[salvo(schema(example = "test"), parameter(description = "标题"))]
    pub title: String,

    #[salvo(schema(example = "test content"))]
    pub content: String,

    #[salvo(schema(example = 1))]
    pub category_id: i32,
}
```

## generated code


You need to implement the two operations of adding and modifying yourself

```Rust
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

  const onFinish = async (values: PropInitValue) => {
    if(isUpdate) {
      // Todo! update
    }else{
      // ToDo! add
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