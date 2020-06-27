# vu3-ui
vue3.0开发的PC端组件库

## Button
```js
import components from 'vu3-ui'
import 'vu3-ui/lib/vu3ui.css'
export default {
	name: 'App',
	components: { ...components },
	setup() {
		return {}
	}
}
```

```vue
<v3-button type="primary" nativeType="button" icon="database-fill" @click="click" plain>确认</v3-button>
```