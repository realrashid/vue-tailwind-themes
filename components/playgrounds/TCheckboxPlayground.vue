<template>
  <playground
    component-name="TCheckbox"
    :settings.sync="settings"
    :theme-builder-settings="themeBuilderSettings"
    :variant="variant"
  >
    <template slot="controls">
      <fieldset>
        <t-input-group variant="playground">
          <label
            for="wrapped"
            class=" flex"
          >
            <t-checkbox
              id="wrapped"
              v-model="wrapped"
              name="wrapped"
              class="form-checkbox h-4 w-4 text-orange-600 transition duration-150 ease-in-out mt-1"
            />

            <div class="ml-3">
              <strong class="block text-sm font-medium text-gray-700 capitalize">
                Wrapped
              </strong>
              <span class="text-sm text-gray-500 leading-none block">Wraps the radio tag in a div, add some extra HTML that make the element more customizable and accepts a label.</span>
            </div>

          </label>
        </t-input-group>

        <t-input-group
          variant="playground"
          :label="themeWasChanged ? 'Custom variants' : 'Example variants'"
        >
          <div class="flex flex-wrap items-center -mx-3">
            <label
              key="---"
              for="variant---"
              class="px-3 py-2 flex items-center "
            >
              <input
                id="variant---"
                v-model="variant"
                :value="''"
                name="variant"
                type="radio"
                class="form-radio h-4 w-4 text-orange-600 transition duration-150 ease-in-out"
              >

              <span class="block text-sm leading-5 font-medium text-gray-700 ml-3 capitalize">
                Default
              </span>
            </label>

            <label
              v-for="(v, variantName) in settings.variants"
              :key="variantName"
              :for="`variant-${variantName}`"
              class="px-3 py-2 flex items-center "
            >
              <input
                :id="`variant-${variantName}`"
                v-model="variant"
                :value="variantName"
                name="variant"
                type="radio"
                class="form-radio h-4 w-4 text-orange-600 transition duration-150 ease-in-out"
              >

              <span class="block text-sm leading-5 font-medium text-gray-700 ml-3 capitalize">
                {{ variantName }}
              </span>
            </label>
          </div>
        </t-input-group>
      </fieldset>
    </template>
  </playground>
</template>

<script>
import cloneDeep from 'lodash/cloneDeep'
import ComponentPlayground from './ComponentPlayground'

const themeBuilderSettings = {
  notWrappedTheme: {
    fixedClasses: 'form-checkbox transition duration-150 ease-in-out',
    classes: '',
    variants: {
      error: 'text-red-500 ',
      success: 'text-green-500 ',
      orange: 'text-orange-500 '
    }
  },
  wrappedTheme: {
    wrapped: true,
    classes: {
      label: '',
      labelChecked: '',
      wrapper: 'mx-1 bg-white border border-gray-300 flex items-center px-4 py-2 rounded shadow-sm cursor-pointer focus:shadow-outline text-sm text-gray-700 hover:text-gray-500 leading-5 uppercase',
      wrapperChecked: 'mx-1 bg-gray-100 border border-gray-300 flex items-center px-4 py-2 rounded shadow-inner cursor-pointer focus:shadow-outline text-sm text-gray-700 hover:text-gray-500 leading-5 uppercase',
      inputWrapper: '',
      inputWrapperChecked: '',
      input: 'absolute invisible'
    },
    variants: {
      error: {
        label: '',
        labelChecked: '',
        wrapper: 'mx-1 bg-red-100 border border-red-200 flex items-center px-4 py-2 rounded shadow-sm cursor-pointer focus:shadow-outline text-sm text-red-700 hover:text-red-500 leading-5 uppercase',
        wrapperChecked: 'mx-1 bg-red-500 border border-red-500 flex items-center px-4 py-2 rounded shadow-inner cursor-pointer focus:shadow-outline text-sm text-red-100 hover:text-red-200 leading-5 uppercase',
        inputWrapper: '',
        inputWrapperChecked: '',
        input: 'absolute invisible'
      },
      success: {
        label: '',
        labelChecked: '',
        wrapper: 'mx-1 bg-green-100 border border-green-200 flex items-center px-4 py-2 rounded shadow-sm cursor-pointer focus:shadow-outline text-sm text-green-700 hover:text-green-500 leading-5 uppercase',
        wrapperChecked: 'mx-1 bg-green-500 border border-green-500 flex items-center px-4 py-2 rounded shadow-inner cursor-pointer focus:shadow-outline text-sm text-green-100 hover:text-green-200 leading-5 uppercase',
        inputWrapper: 'absolute invisible',
        inputWrapperChecked: '',
        input: 'absolute invisible'
      },
      simple: {
        wrapper: 'flex items-center',
        wrapperChecked: 'flex items-center',
        label: 'text-sm uppercase mx-2 text-gray-700',
        labelChecked: 'text-sm uppercase mx-2 text-gray-700',
        inputWrapper: '',
        inputWrapperChecked: '',
        input: 'form-checkbox transition duration-150 ease-in-out'
      }
    }
  }
}

export default ComponentPlayground.extend({
  data () {
    return {
      variant: '',
      wrapped: false,
      themeBuilderSettings,
      settings: cloneDeep(themeBuilderSettings.notWrappedTheme)
    }
  },

  watch: {
    wrapped (wrapped) {
      if (wrapped) {
        this.settings = cloneDeep(themeBuilderSettings.wrappedTheme)
      } else {
        this.settings = cloneDeep(themeBuilderSettings.notWrappedTheme)
      }
    },
    'settings.wrapped' (wrapped) {
      this.wrapped = !!wrapped
    }
  }
})
</script>
