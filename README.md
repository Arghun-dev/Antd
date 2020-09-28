# Antd

### Change Locale

To change the `locale` of the Antd:

App.js (top Parent component)

```js
import { ConfigProvider } from 'antd';
import fa_IR from 'antd/es/locale/fa_IR';
import moment from 'moment';
import 'moment/locale/fa';


// ============Localization of Antd============
moment.locale('fa');

constructor(props) {
    super(props);

    this.state = {
      locale: fa_IR,
    }
  }

render() {
    const { locale } = this.state;
    return (
      <div className="App">
        <ConfigProvider locale={locale}>
          <Provider store={store}>
            <BrowserRouter>
              <PopupChangePassword />
              <PopupForgetPassword />
              <React.Suspense fallback={loading()}>
                <Switch>
                  <Route exact path="/" component={Login} />
                  <Route exact path="/dashboard" component={Dashboard} />
                </Switch>
              </React.Suspense>
            </BrowserRouter>
          </Provider>
        </ConfigProvider>
      </div>
    );
  }
```

### Change Direction

Exactly same local. just add this

```js
constructor(props) {
    super(props);

    this.state = {
      locale: fa_IR,
      direction: 'rtl'
    }
  }
  
  render() {
    <ConfigProvider locale={locale} direction={direction}>
  } 
```

### Using Form (beautiful layout)

**always give this style to have beautiful layout in your page**
imagine you have a `Row` with two `columns`

```js

const formItemLayout = {
    wrapperCol: {
      span: 14
    }
  }


<Form
      style={{ width: '100%' }}
      name="validate_other"
      {...formItemLayout}
      // onFinish={onFinish}
      initialValues={{
        'input-number': 3,
        'checkbox-group': ['A', 'B'],
        rate: 3.5
      }}
    >
      <div className={classes.mainRowDiv}>
        <Row className={classes.firstRow}>
          <Col xs={24} md={12}>
            <Form.Item
              className={classes.formItem}
              name="productName"
              label="نام کالا"
              hasFeedback
              rules={[
                {
                  required: true,
                  message: 'لطفا نام کالا را وارد کن!'
                }
              ]}
            >
              <Input
                type="text"
                placeholder="نام کالا"
                value={productName}
                onChange={(e) => setProductName(e.target.value)}
              />
            </Form.Item>
            <Form.Item
              className={classes.formItem}
              name="productLatinName"
              label="نام لاتین کالا"
              hasFeedback
              rules={[
                {
                  required: true,
                  message: 'لطفا نام لاتین کالا را وارد کن!'
                }
              ]}
            >
              <Input
                type="text"
                placeholder="نام لاتین کالا"
                value={productLatinName}
                onChange={(e) => setProductLatinName(e.target.value)}
              />
            </Form.Item>
            </Col>
            <Col md={12} xs={24}>
                <Form.Item
                  className={classes.formItem}
                  name="productCategory"
                  label="طبقه بندی"
                  hasFeedback
                  rules={[
                    {
                      required: true,
                      message: 'لطفا طبقه بندی کالا را انتخاب کنید!'
                    }
                  ]}
                >
                  <Select
                    showSearch
                    optionFilterProp="children"
                    filterOption={(input, option) =>
                      option.children
                        .toLowerCase()
                        .indexOf(input.toLowerCase()) >= 0
                    }
                    placeholder="طبقه بندی کالا"
                    value={productCategoryId}
                    onChange={(val) => setProductCategoryId(val)}
                  >
                    {productCategories.map((productCategory) => (
                      <Option value={productCategory.categoryId}>
                        {productCategory.categoryName}
                      </Option>
                    ))}
                  </Select>
                </Form.Item>
                <Form.Item
                  className={classes.formItem}
                  name="genericCode"
                  label="کد ژنریک"
                  hasFeedback
                >
                  <Input.Search
                    enterButton
                    type="text"
                    value={genericCode}
                    onChange={(e) => setGenericCode(e.target.value)}
                    placeholder="کد ژنریک"
                    loading={genericCodeSearchLoading}
                    onSearch={() => {
                      setGenericCodeSearchLoading(true)
                      setTimeout(() => {
                        genericCodes.map((item) => {
                          if (item.genericCode === genericCode) {
                            setGenericCodeFound(true)
                            setShowGenericCodeList(false)
                          } else if (item.genericCode !== genericCode) {
                            setShowGenericCodeList(true)
                            setGenericCodeFound(false)
                          }
                        })
                        setGenericCodeSearchLoading(false)
                      }, 2000)
                    }}
                  />
                </Form.Item>
            </Col>
           </Row>
          </div>
```

**styles**

```js
mainRowDiv: {
    display: 'flex',
    justifyContent: 'space-between'
  },
formItem: {
    display: 'flex',
    justifyContent: 'flex-end'
}
```


### making antd dropdown select scroll section fixed not moveable

**just add this line to `Select`**

```js
<Select
    getPopupContainer={(trigger) => trigger.parentNode}
>
</Select>
```

### Clear form fields of antd after submitting the form

**In a function component, you can very easily get access to the form using the Form.useForm hook. The value returned by this hook should be passed as the form property of the Form component. Then you can just call resetFields on the form in whatever callback you want to clear the form. This example will clear the form when it is submitted**

```js
import React from 'react';
import { Button, Form, Input } from 'antd';

export default function MyFormComponent() {
  const [form] = Form.useForm();

  const submitForm = ({ name, favoriteColor }) => {
    console.log(name, favoriteColor);
    form.resetFields();
  };

  return (
    <Form
      form={form}
      labelCol={{ span: 6 }}
      wrapperCol={{ span: 12 }}
      onFinish={submitForm}
    >
      <Form.Item name="name" label="What is your name?">
        <Input />
      </Form.Item>
      <Form.Item name="favoriteColor" label="What is your favorite color?">
        <Input />
      </Form.Item>
      <Form.Item wrapperCol={{ offset: 6, span: 12 }}>
        <Button type="primary" htmlType="submit">
          Submit
        </Button>
      </Form.Item>
    </Form>
  );
}
```
