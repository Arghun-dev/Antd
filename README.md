# Antd

### Tip 1

To change the `locale` of the Antd:

App.js (top Parent component)

```js
import { ConfigProvider } from 'antd';
import fa_IR from 'antd/es/locale/fa_IR';
import moment from 'moment';
import 'moment/locale/fa';


// ============Localization of Antd============
moment.locale('fa');

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
