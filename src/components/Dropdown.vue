<template>
<div
	ref="dropdown"
	:class="'dropdownClass'"
	@click="dropdownClick"
>
	<slot />
</div>
</template>

<script>
import selfInstall from '../utils/selfInstall.js'
export default {
	name: 'Dropdown',

	install(Vue, theme) {
		selfInstall(Vue, theme, this)
	},

	props: {
		tagName: {
			type: String,
			default: 'div'
		},
		buttonTagName: {
			type: String,
			default: 'button'
		},
		variant: {
			type: String,
			default: null,
			validator: function (value) {
				return value === null || ['primary', 'secondary', 'tertiary', 'danger', 'warning', 'success'].indexOf(value) !== -1
			}
		},
		size: {
			type: String,
			default: null,
			validator: function (value) {
				return value === null || ['lg', 'sm'].indexOf(value) !== -1
			}
		},
		text: {
			type: String,
			default: ''
		},
		disabled: {
			type: Boolean,
			default: false
		},
		delayOnMouseOver: {
			type: Number,
			default: 10
		},
		delayOnMouseOut: {
			type: Number,
			default: 10
		},
		appendToBody: {
			type: Boolean,
			default: false
		},
		placement: {
			type: String,
			default: 'auto'
		},
		options: {
			type: Object,
			default: () => {}
		},
		trigger: {
			type: String,
			default: 'click'
		},
		visibleArrow: {
			type: Boolean,
			default: true
		},
		forceShow: {
			type: Boolean,
			default: false
		},
		enterActiveClass: {
			type: String,
			default: null
		},
		leaveActiveClass: {
			type: String,
			default: null
		},
		transition: {
			type: String,
			default: ''
		},
		stopPropagation: {
			type: Boolean,
			default: false
		},
		preventDefault: {
			type: Boolean,
			default: false
		},
		closeOnDropdownClick: {
			type: Boolean,
			default: true
		},
		baseClass: {
			type: [String, Object, Array],
		},
		dropdownClass: {
			type: [String, Object, Array],
		},
		disabledClass: {
			type: [String, Object, Array],
		},
		buttonProps: {
			type: Object,
			default: () => {}
		},
	},

	data () {
		return {
			rerenderKey: 1,
			shown: false
		}
	},

	computed: {
		allOptions () {
			return {
				...this.options,
				...{
					placement: this.placement
				}
			}
		},
		/**
		 * The default classes for the button
		 *
		 * @return {Array}
		 */
		currentClass () {
			let classes = [
				`${this.$options._componentTag}`,
			]

			if (this.baseClass) {
				classes.push(this.baseClass)
			}

			if (this.disabled) {
				classes.push(`${this.$options._componentTag}-disabled`)
				if (this.disabledClass) {
					classes.push(this.disabledClass)
				}
			}

			return classes
		}
	},

	watch: {
		allOptions: {
			handler() {
				this.resetPopper();
			},
			deep: true
		},
	},

	methods: {
		dropdownClick (e) {
			this.$emit('dropdown-click', e)

			if (this.closeOnDropdownClick && this.$refs.popper) {
				this.$refs.popper.doClose()
			}
		},

		onShow (e) {
			this.shown = true
			this.$emit('show', e)
		},

		onHide (e) {
			this.shown = false
			this.$emit('hide', e)
		},
		/**
		 * Change the key forces to the component to re-render
		 * @TODO Make a PR in the vue-popper package for reset the values
		 */
		async resetPopper () {
			this.rerenderKey++
		}
	}
}
</script>
