<template>
  <div id="converter">
    <div class="items">
      <div>
				<input v-model.lazy="value_from_computed" v-money3="moneyMaskConfig" />
      </div>
      <div>
        <select id="convert_from" name="convert_from" v-model="convert_from_computed">
          <option value="" disabled selected>Convert from</option>
          <option value="USD">USD</option>
          <option value="EUR">EUR</option>
          <option value="JPY">JPY</option>
          <option value="GBP">GBP</option>
          <option value="AUD">AUD</option>
          <option value="CAD">CAD</option>
          <option value="CHF">CHF</option>
          <option value="CNY">CNY</option>
          <option value="SEK">SEK</option>
          <option value="NZD">NZD</option>
          <option value="MXN">MXN</option>
          <option value="SGD">SGD</option>
          <option value="HKD">HKD</option>
          <option value="NOK">NOK</option>
          <option value="KRW">KRW</option>
          <option value="TRY">TRY</option>
          <option value="RUB">RUB</option>
          <option value="INR">INR</option>
          <option value="BRL">BRL</option>
          <option value="ZAR">ZAR</option>
          <option value="PHP">PHP</option>
          <option value="THB">THB</option>
          <option value="HUF">HUF</option>
          <option value="DKK">DKK</option>
          <option value="IDR">IDR</option>
          <option value="ILS">ILS</option>
          <option value="MYR">MYR</option>
          <option value="RON">RON</option>
          <option value="CZK">CZK</option>
        </select>
      </div>
      <div>
        <button @click="convertRequest">
          Converter
          <svg xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 640 512">
            <path
              d="M535 41c-9.4-9.4-9.4-24.6 0-33.9s24.6-9.4 33.9 0l64 64c4.5 4.5 7 10.6 7 17s-2.5 12.5-7 17l-64 64c-9.4 9.4-24.6 9.4-33.9 0s-9.4-24.6 0-33.9l23-23L384 112c-13.3 0-24-10.7-24-24s10.7-24 24-24l174.1 0L535 41zM105 377l-23 23L256 400c13.3 0 24 10.7 24 24s-10.7 24-24 24L81.9 448l23 23c9.4 9.4 9.4 24.6 0 33.9s-24.6 9.4-33.9 0L7 441c-4.5-4.5-7-10.6-7-17s2.5-12.5 7-17l64-64c9.4-9.4 24.6-9.4 33.9 0s9.4 24.6 0 33.9zM96 64H337.9c-3.7 7.2-5.9 15.3-5.9 24c0 28.7 23.3 52 52 52l117.4 0c-4 17 .6 35.5 13.8 48.8c20.3 20.3 53.2 20.3 73.5 0L608 169.5V384c0 35.3-28.7 64-64 64H302.1c3.7-7.2 5.9-15.3 5.9-24c0-28.7-23.3-52-52-52l-117.4 0c4-17-.6-35.5-13.8-48.8c-20.3-20.3-53.2-20.3-73.5 0L32 342.5V128c0-35.3 28.7-64 64-64zm64 64H96v64c35.3 0 64-28.7 64-64zM544 320c-35.3 0-64 28.7-64 64h64V320zM320 352a96 96 0 1 0 0-192 96 96 0 1 0 0 192z"
            />
          </svg>
        </button>
      </div>
      <div>
        <select id="convert_to" name="convert_to" v-model="convert_to_computed">
          <option value="" disabled selected>Convert to</option>
          <option value="USD">USD</option>
          <option value="EUR">EUR</option>
          <option value="JPY">JPY</option>
          <option value="GBP">GBP</option>
          <option value="AUD">AUD</option>
          <option value="CAD">CAD</option>
          <option value="CHF">CHF</option>
          <option value="CNY">CNY</option>
          <option value="SEK">SEK</option>
          <option value="NZD">NZD</option>
          <option value="MXN">MXN</option>
          <option value="SGD">SGD</option>
          <option value="HKD">HKD</option>
          <option value="NOK">NOK</option>
          <option value="KRW">KRW</option>
          <option value="TRY">TRY</option>
          <option value="RUB">RUB</option>
          <option value="INR">INR</option>
          <option value="BRL">BRL</option>
          <option value="ZAR">ZAR</option>
          <option value="PHP">PHP</option>
          <option value="THB">THB</option>
          <option value="HUF">HUF</option>
          <option value="DKK">DKK</option>
          <option value="IDR">IDR</option>
          <option value="ILS">ILS</option>
          <option value="MYR">MYR</option>
          <option value="RON">RON</option>
          <option value="CZK">CZK</option>
        </select>
      </div>
    </div>
    <div>
      <h4>Converted Value</h4>
      <h3>{{value_to_formated}}</h3>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue"
import { Money3Directive } from "v-money3"

export default defineComponent ({
	data() {
		return {
			convert_from : "",
			convert_to : "",
			value_from : 0,
			value_from_formated : "",
			value_to : 0,
			value_to_formated : "0,00",
			moneyMaskConfig: {
				masked: false,
				prefix: "",
				suffix: "",
				thousands: ".",
				decimal: ",",
				precision: 2,
				disableNegative: true,
				disabled: false,
				min: null,
				max: null,
				allowBlank: false,
				minimumNumberOfCharacters: 0,
				shouldRound: true,
				focusOnRight: false,
			}
		}
	},
	directives: { money3: Money3Directive.value },
	computed: {
		convert_from_computed: {
			get(): string {
				return this.convert_from
			},
			set(newValue: string) {
				this.convert_from = newValue
			}
		},
		convert_to_computed: {
			get(): string {
				return this.convert_to
			},
			set(newValue: string) {
				this.convert_to = newValue
			}
		},
		value_from_computed: {
			get(): number {
				return this.value_from
			},
			set(newValue: number) {
				this.value_from = newValue
			}
		},
		value_from_formated_computed: {
			get(): string {
				return this.value_from_formated
			},
			set(newValue: string) {
				this.value_from_formated = newValue
			}
		},
		value_to_computed: {
			get(): number {
				return this.value_to
			},
			set(newValue: number) {
				this.value_to = newValue
			}
		},
		value_to_formated_computed: {
			get(): string {
				return this.value_to_formated
			},
			set(newValue: string) {
				this.value_to_formated = newValue
			}
		},
		
	},
	methods: {
		async postData() {
			const url = "https://v6.exchangerate-api.com/v6/4861d10cb9f5243eb1826e4a/latest/" + this.convert_from
			const response = await fetch (url, {
				method: "GET",
				headers: {
					"Content-Type": "application/json",
				},
			})
			const data = await response.json()
			const currencies = data.conversion_rates
			var converted: number = (currencies[this.convert_to] * parseFloat(this.value_from_formated))
			this.value_to_formated = this.convert_to + " " + converted.toLocaleString("pt-BR", {minimumFractionDigits: 2, maximumFractionDigits: 2})
		},
		convertRequest() {
			this.value_from_formated = this.value_from.toString().replace(".", "").replace(",", ".")
			if (this.convert_from !== "" && this.convert_to !== "" && this.value_from !== 0) {
				this.value_from_formated = this.value_from.toString().replace(".", "").replace(",", ".")
				this.postData()
			} else {
				const modal = document.querySelector("#modal")
				modal?.classList.add("opened")
			}
		}	
	},
})
</script>
