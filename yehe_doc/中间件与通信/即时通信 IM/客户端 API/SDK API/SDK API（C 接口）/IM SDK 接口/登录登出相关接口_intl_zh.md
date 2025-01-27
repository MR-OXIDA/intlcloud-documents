## TIMLogin

登录。

**原型**

```c
TIM_DECL int TIMLogin(const char* user_id, const char* user_sig, TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| user_id | const char\* | 用户的 UserID |
| user_sig | const char\* | 用户的 UserSig |
| cb | TIMCommCallback | 登录成功与否的回调。登录时票据过期会返回 ERR_USER_SIG_EXPIRED（6206）或者 ERR_SVR_ACCOUNT_USERSIG_EXPIRED（70001） 错误码，此时生成新的 userSig 重新登录。回调函数定义请参见 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550) |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551) |

>?用户登录腾讯后台服务器后才能正常收发消息，登录需要用户提供 UserID、UserSig 等信息，具体含义请参考 [登录鉴权](https://intl.cloud.tencent.com/document/product/1047/33517)。


## TIMLogout

登出。

**原型**

```c
TIM_DECL int TIMLogout(TIMCommCallback cb, const void* user_data);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| cb | TIMCommCallback | 登出成功与否的回调。回调函数定义请参考 [TIMCommCallback](https://intl.cloud.tencent.com/document/product/1047/34550) |
| user_data | const void\* | 用户自定义数据，IM SDK 只负责传回给回调函数 cb，不做任何处理 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回 TIM_SUCC 表示接口调用成功（接口只有返回 TIM_SUCC，回调 cb 才会被调用），其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551) |

>?如用户主动登出或需要进行用户的切换，则需要调用登出操作。


## TIMGetLoginStatus

获取登录状态。

**原型**

```c
TIM_DECL TIMLoginStatus TIMGetLoginStatus();
```

**返回值**

| 类型 | 含义 |
|-----|-----|
| TIMLoginStatus | 每个返回值的定义请参考 [TIMLoginStatus](https://intl.cloud.tencent.com/document/product/1047/34551) |

>?如果用户已经处于已登录和登录中状态，请勿再频繁调用登录接口登录。


## TIMGetLoginUserID

获取登陆用户的 userID。

**原型**

```c
TIM_DECL int TIMGetLoginUserID(char* user_id_buffer);
```

**参数**

| 参数 | 类型 | 含义 |
|-----|-----|-----|
| user_id_buffer | char* | 用户 ID ，分配内存大小不能低于 128 字节，调用接口后，可以读取到以 '\0' 结尾的字符串 |

**返回值**

| 类型 | 含义 |
|-----|-----|
| int | 返回TIM_SUCC表示接口调用成功，其他值表示接口调用失败。每个返回值的定义请参考 [TIMResult](https://intl.cloud.tencent.com/document/product/1047/34551) |

**示例**

```c
const size_t kUserIDLength = 128;
char user_id_buffer[kUserIDLength] = {0};
TIMGetLoginUserID(user_id_buffer);
```
