
## API

### Form

| 参数 | 说明 | 类型 | 默认值 | 版本 |
| --- | --- | --- | --- | --- |
| form | 经 `autoFormCreate` 属性包装过的组件会自带 `this.form` 属性，直接传给 Form 即可。无需手动设置 | object | 无 |
| hideRequiredMark | 隐藏所有表单项的必填标记就是红色的* | Boolean | false |
| layout | 表单布局 | 'horizontal'\|'vertical'\|'inline' | 'horizontal' |
| autoFormCreate | 自动创建表单`:autoFormCreate="(form)=>{this.form = form}"`,如果有多个表单 `this.form`可设置为`this.form1` |Function(form)| 无|
| labelCol | 在Form上统一设置 label 宽度，用法详见 `FormItem.labelCol`，同时设置时以`FormItem.labelCol`为准 | object | {span:6} |
| wrapperCol | 在Form上统一设置输入控件宽度，用法详见 `FormItem.wrapperCol`，同时设置时以`FormItem.wrapperCol`为准 | object | {span:18} |
| labelWidth | 在Form上统一设置label宽度，同时设置时以`FormItem.labelWidth`为准 | string\|number | - |
| formLayout | 表单栅格布局， 将Form等分为24份，通过 `FormItem.span`设置每个表单所占宽度，注：对`layout='inline'`无效 | boolean | false |
| col | 表单栅格布局时， 将表单分成多少列（col）。注：设置的col必须能整除24，如`1、2、3、4、6、8、12、24`。也可传入object对象，实现响应式表单布局`{xs sm md lg xl xxl}` | number\|object | {  xs: 1, sm: 2, md: 3, lg: 3, xl: 4, xxl: 4 } |
| gutter | 表单栅格布局时， 可通过gutter设置栅格间隔 | number | 0 |
| disabled | 全局禁用当前表单的所有`FormItem`下的表单元素 | boolean | false |
| disabledBorder | 禁用当前表单元素时是否显示border | boolean | true |
| selfUpdate | 自定义字段更新逻辑，你可以通过 Form 的 selfUpdate 进行统一设置。当和 Form 同时设置时，以 Item 为准。 说明见下 需 1.2.8 版本以上  | boolean | true |
| detailEdit | 使用`detail-edit`属性开启详情编辑，可以接收`boolean`、`object`值，如果仅展示详情，则应传入`{edit: false}`,如果需要使用`hover`事件,那么需要传入`{trigger: 'hover',}`，但表单控件不可省略| boolean \| object | false | `@yh/ta404-ui@1.5.155`加入`hover`触发方式,并将其标记为实验性功能 |

**注意:**
- `detailEdit`的`hover`触发方式目前是**实验性**功能!!!
- `detailEdit`如果使用`hover`模式时,目前的组件实现对于下列组件需要额外在组件外部点击一次才能隐藏编辑组件

```
  'TaAutoComplete',
  'TaCascader',
  'TaRate',
  'TaSelect',
  'TaSuggest',
  'TaTimePicker',
  'TaDatePicker',
  'TaMonthPicker',
  'TaQuarterPicker',
  'TaYearPicker',
  'TaRangePicker',
  'TaTreeSelect'
```
- `detailEdit`为`true`时, 默认的触发方式为`click`,如果需要使用`hover`进行触发,则**必须**使用`{trigger: 'hover',}`


### 方法
```js
this.form.XXX()
\\例如:
this.form.getFieldsValue()
```

> 注意：使用 `getFieldsValue` `getFieldValue` `setFieldsValue` 等时，应确保对应的 `form-item` 已经添加了`fieldDecoratorId` 属性。
> 注意：使用 `getFieldsMomentValue` `getFieldMomentValue` 等时，应确保对应的日期组件已经添加了`format` 属性。

| 方法      | 说明                                     | 类型       |
| ------- | -------------------------------------- | -------- |
| getFieldError | 获取某个输入控件的 Error | Function(name) |
| getFieldsError | 获取一组输入控件的 Error ，如不传入参数，则获取全部组件的 Error | Function(\[names: string\[]]) |
| clearFieldError | 清除某个输入控件的 Error | Function(name) |
| clearFieldsError | 清除一组输入控件的 Error ，如不传入参数，则清除全部组件的 Error | Function(\[names: string\[]]) |
| getFieldsValue | 获取一组输入控件的值，如不传入参数，则获取全部组件的值 | Function(\[fieldNames: string\[]]) |
| getFieldsMomentValue | 获取一组输入控件（特指日期组件）的值，如不传入参数，则获取全部组件的值 | Function(\[fieldNames: string\[]]) |
| getFieldsSensitiveValue | 获取一组输入控件的脱敏值(需要设置控件的`sensitive`参数), 如果不传入参数, 则获取全部组件的值 | Function(\[fieldNames: string\[]]) |
| getAllChangeEventArgs | 获取一组输入控件的change事件的参数,若不传入参数,则获取全部组件的change事件的参数,若组件还没有触发change事件,那么将会返回undefined | Function(\[fieldNames: string\[]]) |
| getFieldValue | 获取一个输入控件的值 | Function(fieldName: string) |
| getFieldMomentValue | 获取一个输入控件（特指日期组件）的值 | Function(fieldName: string) |
| getFieldSensitiveValue | 获取一个输入控件的脱敏值(需要设置控件的`sensitive`参数) | Function(fieldName: string) |
| isFieldsTouched | 输入控件,输入值后才会返回true,主要是用在做验证的时候,用来判断用户是否输入,有输入改变才进行下一步工作| (names?: string\[]) => boolean |
| isFieldTouched | 判断一个输入控件,输入值后才会返回true,主要是用在做验证的时候,用来判断用户是否输入,有输入改变才进行下一步工作 | (name: string) => boolean |
| isFieldValidating | 判断一个输入控件是否在校验状态,(就是在输入框后面转圈圈状态) | Function(name) |
| resetFields | 重置一组输入控件的值（为 `initialValue`）与状态，如不传入参数，则重置所有组件 | Function(\[names: string\[]]) |
| setFields | 设置一组输入控件的值与 Error。 | Function({ [fieldName]&#x3A; { value: any, errors: [Error] } }) |
| setFieldsValue | 设置一组输入控件的值 | Function({ [fieldName]&#x3A; value } |
| setFieldsMomentValue | 设置一组输入控件（日期组件）的值,这个值接受字符串或者字符串数组。若有需要可以设置组件的format属性 | Function({ [fieldName]&#x3A; value } |
| validateFields | 校验并获取一组输入域的值与 Error，若 fieldNames 参数为空，则校验全部组件` this.form.validateFields([fieldNames: string[]], [options: object], callback: Function(errors, values))` ,注意使用框架的this.submit的autoValid=true这个属性,那么就会自动帮你验证,不用自己去调用验证| Function(\[fieldNames: string\[]], [options: object], callback: Function(errors, values)) |
| validateFieldsAndScroll | 与 `validateFields` 相似,用法一样，但校验完后，如果校验不通过的菜单域不在可见范围内，则自动滚动进可见范围 | 参考 `validateFields` |

### validateFields的options参数
```js
this.form.validateFields([fieldDecoratorId1,fieldDecoratorId2...],options,(errors, values)=>{})
this.form.validateFieldsAndScroll([fieldDecoratorId1,fieldDecoratorId2...],options,(errors, values)=>{})
```
| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| options.first | 若为 true，则每一表单域的都会在碰到第一个失败了的校验规则后停止校验 | boolean | false |
| options.firstFields | 指定表单域会在碰到第一个失败了的校验规则后停止校验 | String\[] | \[] |
| options.force | 对已经校验过的表单域，在 validateTrigger 再次被触发时是否再次校验 | boolean | false |
| options.scroll | 定义 validateFieldsAndScroll 的滚动行为，详细配置见 [dom-scroll-into-view config](https://github.com/yiminghe/dom-scroll-into-view#function-parameter) | Object | {} |
| options.focus | 是否对第一个校验失败的表单项自动 focus , 使用 validateFieldsAndScroll 方法时可用 | boolean | false |

### Form.Item

**注意:**
1. 你**不再需要也不应该**用 `onChange` 来做设置组件的value值，但还是可以继续监听 `onChange` 等事件。
2. 你不能用控件的 `value` `defaultValue` 等属性来设置表单域的值，默认值可以用`initialValue`。
3. 你不应该用控件的 `v-model`，可以使用 `this.form.setFieldsValue` 来动态改变表单值。
4. 一个 Form.Item 建议只放一个表单组件，当放多个表单组件时，`help` `required` `validateStatus` 无法自动生成。
5. 注意compare属性目前必须传入一个json对象，同时，需要设置validateStatus、help属性，并且，在callback回调中设置其验证后的属性值
6. 如果使用`require`属性,必须要设置`fieldDecoratorId`
7. 需要注意，`Form`和`FormItem`组件都包含一个`disabled`属性；不同的是，`Form`的`disabled`属性存在默认值。若要同时使用`Form`和`FormItem`的`disabled`属性，则需要注意的是：
    1. 如果同时使用了两个组件的`disabled`属性，则`FormItem`的`disabled`属性会强制**覆盖**`Form`组件的`disabled`属性。
    1. 当且仅当`FormItem`的`disabled`属性为`undefined`时，`Form`的`disabled`属性才会生效。

| 参数 | 说明 | 类型 | 默认值 | 版本 |
| --- | --- | --- | --- | --- |
| colon | 配合 label 属性使用，表示是否显示 label 后面的冒号 | boolean | true | - |
| extra | 额外的提示信息，和 help 类似，当需要错误信息和提示文案同时出现时，可以使用这个。 | string\|slot |  | - |
| hasFeedback | 配合 validateStatus 属性使用，展示校验状态图标，建议只配合 Input 组件使用 | boolean | false | - |
| help | 提示信息，如不设置，则会根据校验规则自动生成 | string\|slot |  | - |
| label | label 标签的文本 | string\|slot |  | - |
| labelCol | label 标签布局，同 `<Col>` 组件，设置 `span` `offset` 值，如 `{span: 3, offset: 12}` 或 `sm: {span: 3, offset: 12}` | object | {span:6} | - |
| labelWidth | label宽度 | string\|number | - | - |
| span | 使用表单布局`:formLayout='true'`时，栅格占位格数。也可传入object对象，实现响应式表单布局`{xs sm md lg xl xxl}` | number\|object |  | - |
| requireStatus | 是否显示必填项目的红色星星;具体使用详情请参照`requiedStatus属性说明`示例(从`1.5.152`起用于替代`required`属性) | boolean | false | 1.5.152 |
| required | 不推荐使用,与`requireStatus`行为完全一致,但是`requireStatus`优先级高于`required`,且仅当`requireStatus`为`undefined`(未设置或值为`undefined`)时其才有效.由于其命名与`require`属性相似,所以从`1.5.152`开始弃用,避免与`require`属性混淆,保留此属性只是为了确保`1.5.*`版本兼容,不推荐使用. | - | - | 1.5.152起弃用 |
| requireMessage | 字段的验证消息.如果设置了这个属性就说明要进行字段验证.且如果设置了这个属性,那么`requireStatus`属性的默认值将变为`true`;具体使用详情请参照 `requireMessage属性说明`示例(从`1.5.152`起用于替代`require`属性) | object\|boolean | - | 1.5.152 |
| require | 不推荐使用,与`requireMessage`行为完全一致,但是`requireMessage`优先级高于`require`,且仅当`requireMessage`为`undefined`(未设置或值为`undefined`)时其才有效.由于其命名与`required`属性相似,所以从`1.5.152`开始弃用,避免与`required`属性混淆,保留此属性只是为了确保`1.5.*`版本兼容,不推荐使用. | - | - | 1.5.152起弃用 |
| validateStatus | 校验状态，如不设置，则会根据校验规则自动生成，可选：'success' 'warning' 'error' 'validating' | string | - | - |
| wrapperCol | 需要为输入控件设置布局样式时，使用该属性，用法同 labelCol | object | {span:18} | - |
| fieldDecoratorId | 表单组件识别id,如果需要获取到该组件的值,那么必须设置 | string | 无 | - |
| fieldDecoratorOptions | 表单组件的传入参数,这里可以设置组件的初始值等 | object | {} | - |
| compare | 两个表单组件比较值时使用详情看比较示例compare示例 | object | {targetId:'',rule:'',message:'',callback:function(error:{status:'',help:''}{})} | - |
| initValue | 该字段初始化值,如果写了initValue属性,则显示initValue设置的值,具体使用详情请参照 `formItem initValue属性设置`示例 | object |  | - |
| valuePropName | 该字段初始化值,若指定了valuePropName则表示这个属性所对应的值表示这个组件的值（用于初始化、获取、设置值等操作）。具体使用详情请参照 `formItem initValue属性设置`示例 | object，默认'value'，可选'checked'等 |  | - |
| disabled | 是否禁用当前表单的表单元素 | boolean,undefined | undefined | - |
| selfUpdate | 自定义字段更新逻辑，你可以通过 Form 的 selfUpdate 进行统一设置。当和 Form 同时设置时，以 Item 为准。 说明见下 需 1.2.8 版本以上  | boolean | true | - |
| showInfo | 是否显示form-item的info,注意,此属性设置为false时会隐藏表单验证的信息显示,需1.5.144版本及以上  | boolean | true | - |
| getLabel | 在`label`设置为`slot`时,且通过`requireMessage`或`require`属性设置了`form-item`必填,可以通过此属性对返回一个`form-item`的`label`值,用于构造验证`require`的必填信息,如果这个属性没有设置,那么验证的必填信息将会使用`fieldDecoratorId`构造;需要1.5.154-1及以上版本  | (fieldDecoratorId)=>label | undefined | 1.5.154-1 |
#### fieldDecoratorOptions 参数
<span style="display:none">
这属性不知道是干嘛的
| getValueFromEvent | 可以把 onChange 的参数（如 event）转化为控件的值 | function(..args) | reference |
</span>

```html
 <ta-form-item
        fieldDecoratorId="myid"
        :fieldDecoratorOptions="{rules: [{ required: true, message: '请输入myid的信息!' }]}"
      >
        <ta-input/>
</ta-form-item>
```

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| initialValue | 子节点的初始值 |  |  |
| normalize | 对value做处理返回新的value值,比如: `function(value, prevValue, allValues){return value+'喵' }`这里你输入`猫`那么输入框最后显示的为`猫喵`| function(value, prevValue, allValues): any | - |
| rules | 校验规则，参考下方文档 | object\[] |  |
| trigger | 收集子节点的值的时机 | string | 'change' |
| validateFirst | 当某一规则校验不通过时，是否停止剩下的规则的校验 | boolean | false |
| validateTrigger | 校验子节点值的时机 | string\|string\[] | 'change' |
| valuePropName | 表示FormItem的首个子节点组件设置其值的属性名称，即：若单独使用这个组件时，通过此属性可以控制其值，如 Switch、单独使用的CheckBox/Radio 的是 'checked'，一般为'value'。（各个组件文档里有相应的说明） | string | 'value' |

### 校验规则rules

| 参数 | 说明 | 类型 | 默认值 | 可选值 |
| --- | --- | --- | --- | --- |
| enum | 枚举类型 | string | - | - |
| len | 字段长度 | number | - | - |
| max | 最大长度 | number | - | - |
| message | 校验文案 | string | - | - |
| min | 最小长度 | number | - | - |
| pattern | 正则表达式校验 | RegExp | - | - |
| required | 是否必选 | boolean | `false` | - |
| transform | 校验前转换字段值 | function(value) => transformedValue:any | - | - |
| type | 内建校验类型（详细API见下方，示例见`内建校验类型`），以及扩展支持('idCard','phone'，表示二代身份证及手机号码，更多自定义验证可使用扩展支持的idCard、phone以及customRule属性） | string | 'string' | - |
| validator | 自定义校验 | function(rule, value, callback) | - | - |
| whitespace | 必选时，空格是否会被视为错误 | boolean | `false` | - |
| idCard | 输入时，会检查输入的内容是否满足（如二代身份证）的校验规则；目前支持二代/香港/澳门身份证。 | string | `2` | '2'\|'hk'\|'mo' |
| phone | 输入时，会按照预设规则检查用户输入内容是否满足其规则；目前仅支持手机号长度验证。 | string | `mobile` | - |

**注意:**

+ 香港/澳门身份证验证需要`@yh/ta-utils@3.0.67`或以上版本

### 校验规则rules.type

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| string | 字符串类型 | string | - |
| number | 字段长度 | number | - |
| boolean | 布尔值类型 | boolean | - |
| enum | 枚举类型 | string | - |
| url | url验证 | string | - |
| email | email验证 | string | - |
| hex | 颜色值验证 | string | - |

### selfUpdate

设置 selfUpdate 为 true 后，Form 通过增量方式更新，只更新被修改的字段。大部分场景下，你只需要编写代码即可。而在某些特定场景，例如修改某个字段值后出现新的字段选项、或者纯粹希望表单任意变化都需要进行渲染。你可以通过修改 Form.Item 取消 selfUpdate，或者在 change / onValuesChange 回调中手动调用 this.$forceUpdate() 更新组件。

如果你并不精通 Vue，并不建议使用 selfUpdate，如果出现性能问题，可以尝试这把 Form 相关的业务独立到一个单独的组件中，减少组件渲染的消耗。
