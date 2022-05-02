<template>
    <v-container>
        <v-data-table v-model="selected" :headers="headers" :items="desserts" item-key="name" show-select
            class="elevation-1" @toggle-select-all="selectAllToggle" @click:row="clickRow">
            <template v-slot:[`item.data-table-select`]="{ item, isSelected, select }">
                <v-simple-checkbox :value="isSelected" :readonly="item.disabled" :disabled="item.disabled"
                    @input="select($event)" :ripple="false"></v-simple-checkbox>
            </template>
        </v-data-table>
    </v-container>
</template>

<script>
export default {
    data() {
        return {
            selected: [],
            disabledCount: 0,
            headers: [
                {
                    text: 'Dessert (100g serving)',
                    align: 'start',
                    sortable: false,
                    value: 'name',
                },
                { text: 'Calories', value: 'calories' },
                { text: 'Fat (g)', value: 'fat' },
                { text: 'Carbs (g)', value: 'carbs' },
                { text: 'Protein (g)', value: 'protein' },
                { text: 'Iron (%)', value: 'iron' },
            ],
            desserts: [],
        }
    },
    methods: {
        selectAllToggle(props) {
            if (this.selected.length != this.desserts.length - this.disabledCount) {
                this.selected = []
                props.items.forEach(item => {
                    if (!item.disabled) this.selected.push(item)
                })
            } else {
                this.selected = []
            }
        },
        clickRow(row) {
            row.disabled = !row.disabled
        }
    },
    created() {
        // dessertsへの値セット
        this.desserts = [
            {
                name: 'Frozen Yogurt',
                calories: 159,
                fat: 6.0,
                carbs: 24,
                protein: 4.0,
                iron: '1%',
                disabled: true
            },
            {
                name: 'Ice cream sandwich',
                calories: 237,
                fat: 9.0,
                carbs: 37,
                protein: 4.3,
                iron: '1%',
                disabled: true
            },
            {
                name: 'Eclair',
                calories: 262,
                fat: 16.0,
                carbs: 23,
                protein: 6.0,
                iron: '7%',
                disabled: false
            },
            {
                name: 'Cupcake',
                calories: 305,
                fat: 3.7,
                carbs: 67,
                protein: 4.3,
                iron: '8%',
                disabled: false
            },
            {
                name: 'Gingerbread',
                calories: 356,
                fat: 16.0,
                carbs: 49,
                protein: 3.9,
                iron: '16%',
                disabled: true
            },
            {
                name: 'Jelly bean',
                calories: 375,
                fat: 0.0,
                carbs: 94,
                protein: 0.0,
                iron: '0%',
                disabled: false
            },
            {
                name: 'Lollipop',
                calories: 392,
                fat: 0.2,
                carbs: 98,
                protein: 0,
                iron: '2%',
                disabled: false
            },
            {
                name: 'Honeycomb',
                calories: 408,
                fat: 3.2,
                carbs: 87,
                protein: 6.5,
                iron: '45%',
                disabled: false
            },
            {
                name: 'Donut',
                calories: 452,
                fat: 25.0,
                carbs: 51,
                protein: 4.9,
                iron: '22%',
                disabled: false
            },
            {
                name: 'KitKat',
                calories: 518,
                fat: 26.0,
                carbs: 65,
                protein: 7,
                iron: '6%',
                disabled: true
            },
        ]
    },
    watch: {
        desserts: {
            handler: function () {
                this.disabledCount = 0
                this.desserts.map(item => {
                    if (item.disabled) this.disabledCount += 1
                })
            },
            deep: true
        }
    }
}
</script>