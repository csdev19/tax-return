<template>
  <div class="container mx-auto">
    <h1
      class="text-3xl uppercase font-bold text-teal-500 text-center mt-5 mb-5"
    >
      Calcular el impuesto a la renta de cuarta categoría
    </h1>

    <div class="mb-3 xl:w-96">
      <label
        for="earned-income"
        class="form-label inline-block mb-2 text-gray-700"
        >Sueldo mensual</label
      >
      <input
        id="earned-income"
        type="number"
        class="form-control block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
        placeholder="Ingrese su ingreso total"
        :value="earnedIncome"
        @input="(event) => (earnedIncome = event.target.value)"
      />
    </div>

    <div>
      <p>
        Pasos a tener en cuenta para calcular los impuestos de 4ta categoria. La
        UIT actual (2022) es: S/ {{ uit }}.
      </p>
    </div>

    <div class="flex flex-col m-auto">
      <div
        class="my-4 flex md:flex-row flex-col justify-center border-solid border-2 border-red-500 rounded-lg bg-teal-200 md:text-left text-center"
      >
        <div class="py-10 flex flex-col w-11/12 rounded bg-teal-200">
          <div class="flex">
            <div class="w-3/5">
              <div class="text-xs uppercase font-bold text-red-500 mb-2">
                <span class="bg-red-500 text-white p-1 rounded-lg">Paso 1</span>
                - Primer descuento
              </div>
              <div class="md:text-xl text-xl font-bold text-red-700">
                Descuenta el {{ firstDiscount }}% de los ingresos percibidos o
                cobrados durante el año
              </div>

              <div class="mt-4 text-red-800">
                Ejemplo: si tuviste S/ 40,000.00 soles de ingresos durante todo
                el año 2021, debes descontar S/ 8,000.00.<br />
                40,000 - 8,000 = S/ 32,000.00.
              </div>
            </div>
            <div class="w-2/5 flex">
              <div
                class="bg-red-500 rounded-lg w-4/5 text-white p-4 inline-block m-auto"
              >
                Entonces calculamos: <br />
                - Con un ingreso total de: {{ earnedIncome }}<br />
                - El descuento de: {{ earnedIncome * (firstDiscount / 100)
                }}<br />
                - Nos queda:
                {{ earnedIncome - earnedIncome * (firstDiscount / 100) }}
              </div>
            </div>
          </div>
        </div>
      </div>
      <div
        class="my-4 flex md:flex-row flex-col justify-center border-solid border-2 border-green-500 rounded-lg bg-orange-200 md:text-left text-center"
      >
        <div class="py-10 flex flex-col w-11/12 rounded bg-orange-200">
          <div class="flex">
            <div class="w-3/5">
              <div class="text-xs uppercase font-bold text-green-500 mb-2">
                <span class="bg-green-500 text-white p-1 rounded-lg"
                  >Paso 2</span
                >
                - Descuento de UIT
              </div>
              <div class="md:text-xl text-xl font-bold text-green-700">
                Descuenta el valor de 7 UIT
              </div>
              <div class="mt-4 text-green-800">
                Resta 7 UIT S/ 30,800.00 del resultado anterior: 32,000 - 30,100
                = S/ 1,200.00.
              </div>
            </div>
            <div class="w-2/5 flex">
              <div
                class="bg-green-500 rounded-lg w-4/5 text-white p-4 inline-block m-auto"
              >
                Entonces calculamos: <br />
                - En base al calculo anterior:
                {{ earnedIncome - earnedIncome * (firstDiscount / 100) }}<br />
                - Le restamos 7 UIT: {{ uit * uitQuantity }}<br />
                - Nos queda:
                {{
                  earnedIncome -
                  earnedIncome * (firstDiscount / 100) -
                  uit * uitQuantity
                }}
              </div>
            </div>
          </div>
        </div>
      </div>
      <div
        class="my-4 flex md:flex-row flex-col justify-center border-solid border-2 border-indigo-500 rounded-lg md:text-left text-center"
      >
        <div class="py-10 flex flex-col w-11/12 rounded">
          <div class="flex">
            <div class="w-3/5">
              <div class="text-xs uppercase font-bold text-indigo-500 mb-2">
                <span class="bg-indigo-500 text-white p-1 rounded-lg"
                  >Paso 3</span
                >
                - Aplicar tasa de impuesto
              </div>
              <div class="md:text-xl text-xl font-bold text-indigo-700">
                Aplica la tasa del impuesto por cada tramo de ingresos
              </div>
              <div class="mt-4 text-indigo-800">
                Rango o tramo de ingresos: Tasa a aplicar. Valor de UIT 2022: S/
                4,400.00.<br /><br />

                - 1er Tramo: de 0 - 5 UIT 8%<br />
                - 2do Tramo: de 5 - 20 UIT 14%<br />
                - 3er Tramo: de 20 - 35 UIT 17%<br />
                - 4to Tramo: de 35 - 45 UIT 20%<br />
                - 5to Tramo: más de 45 UIT 30%<br /><br />
                Como el "monto base" sobre el que se calcula el impuesto se
                encuentra dentro del primer tramo S/ 1,200.00 al ser menor a 5
                UIT S/ 22,000.00, debes aplicar la tasa del 8% es decir 1,200 x
                8% = S/ 96.00. Si el "monto base" fuera mayor, tendrás que
                calcular impuestos por cada tramo, para luego sumar los mismos y
                así obtener el impuesto total.<br />
              </div>
            </div>
            <div class="w-2/5 flex">
              <div
                class="bg-indigo-500 rounded-lg w-4/5 text-white p-4 inline-block m-auto"
              >
                Entonces calculamos: <br />
                - Lo que nos quedaba en base al calculo anterior:
                {{
                  earnedIncome -
                  earnedIncome * (firstDiscount / 100) -
                  uit * uitQuantity
                }}.<br />
                -
                {{
                  getDescriptionBySection()
                    ? `La seccion en la que se encuentra es la ${getDescriptionBySection()}`
                    : 'No se encontro una descripcion'
                }}.<br />
                - El impuesto a pagar es: {{ getTaxBySection() || 0 }}<br />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div>
      <p>
        Referencia en esta pagina del gobierno de Peru
        <a
          href="https://www.gob.pe/7318-calcular-el-impuesto-a-la-renta-de-cuarta-categoria"
          target="_blank"
          >link</a
        >
      </p>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

type TSection = {
  minUit: number
  maxUit: number
  percentage: number
  description: string
}

const sections: TSection[] = [
  {
    minUit: 0,
    maxUit: 5,
    percentage: 8,
    description: '1er tramo de 0 - 5 UIT de 8%',
  },
  {
    minUit: 5,
    maxUit: 20,
    percentage: 14,
    description: '2do tramo de 5 - 20 UIT de 14%',
  },
  {
    minUit: 20,
    maxUit: 35,
    percentage: 17,
    description: '3er tramo de 20 - 35 UIT de 17%',
  },
  {
    minUit: 35,
    maxUit: 45,
    percentage: 20,
    description: '4to tramo de 35 - 45 UIT de 20%',
  },
  {
    minUit: 45,
    maxUit: 10000000,
    percentage: 30,
    description: '5to tramo más de 45 UIT de 30%',
  },
]

export default Vue.extend({
  name: 'CategoryFourPage',
  // components: {
  //   Fouth
  // },
  data: () => {
    return {
      uit: 4_400,
      uitQuantity: 7,
      earnedIncome: 40_000,
      firstDiscount: 20,
      section: null,
    }
  },
  computed: {},
  methods: {
    getSection(amount: number): TSection {
      const [section] = sections.filter(
        (section) =>
          section.minUit * this.uit < amount &&
          section.maxUit * this.uit > amount
      )
      return section
    },
    getTaxBySection() {
      const rest =
        this.earnedIncome -
        this.earnedIncome * (this.firstDiscount / 100) -
        this.uit * this.uitQuantity
      const section = this.getSection(rest)
      return (section?.percentage / 100) * rest
    },
    getDescriptionBySection() {
      const rest =
        this.earnedIncome -
        this.earnedIncome * (this.firstDiscount / 100) -
        this.uit * this.uitQuantity
      const section = this.getSection(rest)
      return section?.description
    },
    getPercentageBySection() {
      const rest =
        this.earnedIncome -
        this.earnedIncome * (this.firstDiscount / 100) -
        this.uit * this.uitQuantity
      const section = this.getSection(rest)
      return section?.percentage
    },
  },
})
</script>
