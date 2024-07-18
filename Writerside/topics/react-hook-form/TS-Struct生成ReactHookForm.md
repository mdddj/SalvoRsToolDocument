# Struct Generate ReactHookForm


> Note: The following functions require adding two front-end frameworks to the front-end project(<a href='https://tailwindcss.com/docs/installation/'>tailwindcss</a>和<a href='https://daisyui.com/'>daisy ui</a>)

> Note: You need to add two React components in the temp window, open and copy them to your react project
> 
![img_hook_form_temp.png](img_hook_form_temp.png)


## start using

![img_hook_form.png](img_hook_form.png)

## example struct





rust 

```Rust
pub struct PermissionAddRequest {
    pub name: String,
    pub description: Option<String>,
    pub create_time: Option<String>,
    pub permission_url: Option<String>
}
```

## Generate form content

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

    //todo!
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

## Result

![img_hook_form_example.png](img_hook_form_example.png)