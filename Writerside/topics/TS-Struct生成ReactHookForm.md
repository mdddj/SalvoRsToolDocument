# TS: Struct生成ReactHookForm


> 注意:下面的功能需要在前端项目中添加两个前端框架(<a href='https://tailwindcss.com/docs/installation/'>tailwindcss</a>和<a href='https://daisyui.com/'>daisy ui</a>)

> 注意: 需要再temp窗口添加两个React组件,打开并拷贝到你的react项目中
> 
![img_hook_form_temp.png](img_hook_form_temp.png)


## 开始使用

![img_hook_form.png](img_hook_form.png)

## 示例 struct





rust 
```Javascript
pub struct PermissionAddRequest {
    ///名称
    pub name: String,
    ///介绍
    pub description: Option<String>,
    ///创建时间
    pub create_time: Option<String>,
    ///访问URL
    pub permission_url: Option<String>
}
```

## 生成表单内容

interface
```Javascript
import React, { JSX } from 'react';
import {
    Controller, useForm,
} from 'react-hook-form';

interface PermissionAddRequest {
	name: string,
	description: string | undefined,
	create_time: string | undefined,
	permission_url: string | undefined,
}


const MyDialog: React.FC<Prop> = (props) => {
    const { register, handleSubmit, reset, control} = useForm<PermissionAddRequest>();

    //todo!提交数据
    const onFinish = async (values: PermissionAddRequest) => {

    };

    return (
        <Dialog id={'my-dialog'} onClose={() => reset()}>
            <DialogBody>
                <DialogTitle title={'表单'} />
                <form onSubmit={handleSubmit(onFinish)}>
                          <Controller render={function({ field, fieldState: { error } }) {
  return <InputWrapper label={'名称'} bottomLeftLabel={error?.message}>
    <input type={'text'} {...field} {...register("name")} className={get_input_class(error?.message)} placeholder={'name'}  />
  </InputWrapper>;
}} name={'name'} control={control} rules={{ required: '请输入名称' }} />

      <Controller render={function({ field, fieldState: { error } }) {
  return <InputWrapper label={'介绍'} bottomLeftLabel={error?.message}>
    <input type={'text'} {...field} {...register("description")} className={get_input_class(error?.message)} placeholder={'description'}  />
  </InputWrapper>;
}} name={'name'} control={control}  />

      <Controller render={function({ field, fieldState: { error } }) {
  return <InputWrapper label={'创建时间'} bottomLeftLabel={error?.message}>
    <input type={'text'} {...field} {...register("create_time")} className={get_input_class(error?.message)} placeholder={'create_time'}  />
  </InputWrapper>;
}} name={'name'} control={control}  />

      <Controller render={function({ field, fieldState: { error } }) {
  return <InputWrapper label={'访问URL'} bottomLeftLabel={error?.message}>
    <input type={'text'} {...field} {...register("permission_url")} className={get_input_class(error?.message)} placeholder={'permission_url'}  />
  </InputWrapper>;
}} name={'name'} control={control}  />


                </form>
            </DialogBody>
            <DialogCloseBtn />
        </Dialog>
    );
};
export { MyDialog };
```

## 效果

![img_hook_form_example.png](img_hook_form_example.png)