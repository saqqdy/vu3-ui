<script>
/**
 * v3-button
 * @module package/button
 * @desc 按钮
 * @param {string} [type=default] - 显示类型，接受 default, primary, danger
 * @param {boolean} [disabled=false] - 禁用
 * @param {boolean} [plain=false] - 幽灵按钮
 * @param {string} [size=normal] - 尺寸，接受 normal, small, large
 * @param {string} [native-type] - 原生 type 属性
 * @param {string} [icon] - 图标，提供 more, back，或者自定义的图标（传入不带前缀的图标类名，最后拼接成 .iconfont-xxx）
 * @param {slot} - 显示文本
 * @param {slot} [icon] 显示图标
 *
 * @example
 * <v3-button size="large" icon="back" type="primary">按钮</v3-button>
 */
import { h } from "vue";
export default {
	name: "v3-button",
	inheritAttrs: false,
	props: {
		icon: String,
		disabled: Boolean,
		nativeType: String,
		plain: Boolean,
		type: {
			type: String,
			default: "default",
			validator(value) {
				return ["default", "danger", "primary"].indexOf(value) > -1;
			},
		},
		size: {
			type: String,
			default: "normal",
			validator(value) {
				return ["small", "normal", "large"].indexOf(value) > -1;
			},
		},
	},
	setup(props, { slots, emit }) {
		const handleClick = (e) => {
			emit("click", e);
		};
		return () => [
			h(
				"button",
				{
					type: props.nativeType,
					class: [
						"v3-button",
						"v3-button--" + props.size,
						"v3-button--" + props.type,
						{
							"is-disabled": props.disabled,
							"is-plain": props.plain,
						},
					],
					onClick: handleClick,
					disabled: props.disabled,
				},
				[
					h(
						"span",
						{
							class: ["v3-button-icon"],
						},
						slots.icon
							? slots.icon()
							: (props.icon &&
									h("i", {
										class: [
											"iconfont",
											"icon-" + props.icon,
										],
									})) ||
									null
					),
					" ",
					h(
						"label",
						{
							class: ["v3-button-text"],
						},
						slots.default()
					),
				]
			),
		];
	},
};
</script>

<style lang="less">
.v3-button {
	-webkit-appearance: none;
	-moz-appearance: none;
	appearance: none;
	border-radius: 4px;
	border: 0;
	box-sizing: border-box;
	color: inherit;
	display: block;
	font-size: 16px;
	height: 41px;
	outline: 0;
	overflow: hidden;
	position: relative;
	text-align: center;
}
.v3-button::after {
	background-color: #000;
	content: " ";
	opacity: 0;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	position: absolute;
}
.v3-button:not(.is-disabled):active::after {
	opacity: 0.4;
}
.v3-button.is-disabled {
	opacity: 0.6;
}
.v3-button-icon {
	vertical-align: middle;
	display: inline-block;
}
.v3-button--default {
	color: #656b79;
	background-color: #f6f8fa;
	box-shadow: 0 0 1px #b8bbbf;
}
.v3-button--default.is-plain {
	border: 1px solid #5a5a5a;
	background-color: transparent;
	box-shadow: none;
	color: #5a5a5a;
}
.v3-button--primary {
	color: #fff;
	background-color: #17c0ae;
}
.v3-button--primary.is-plain {
	border: 1px solid #17c0ae;
	background-color: transparent;
	color: #17c0ae;
}
.v3-button--danger {
	color: #fff;
	background-color: #ef4f4f;
}
.v3-button--danger.is-plain {
	border: 1px solid #ef4f4f;
	background-color: transparent;
	color: #ef4f4f;
}
.v3-button--large {
	display: block;
	width: 100%;
}
.v3-button--normal {
	display: inline-block;
	padding: 0 12px;
}
.v3-button--small {
	display: inline-block;
	font-size: 14px;
	padding: 0 12px;
	height: 33px;
}
</style>
