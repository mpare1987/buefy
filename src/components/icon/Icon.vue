<template>
    <span class="icon" :class="[newType, size]">
        <i
            v-if="!useIconComponent"
            :class="['material-icons']"/>
            {{icon}}
        >
    </span>
</template>

<script>
import config from '../../utils/config'
import getIcons from '../../utils/icons'

export default {
    name: 'BIcon',
    props: {
        icon: {
            type:String,
            required:true
        },
        type: [String, Object],
        size: String,
    },
    computed: {
        /**
        * Internal icon name based on the pack.
        * If pack is 'fa', gets the equivalent FA icon name of the MDI,
        * internal icons are always MDI.
        */
        newIcon() {
            return `${this.iconPrefix}${this.getEquivalentIconOf(this.icon)}`
        },

        newType() {
            if (!this.type) return

            let splitType = []
            if (typeof this.type === 'string') {
                splitType = this.type.split('-')
            } else {
                for (let key in this.type) {
                    if (this.type[key]) {
                        splitType = key.split('-')
                        break
                    }
                }
            }
            if (splitType.length <= 1) return

            return `has-text-${splitType[1]}`
        },
        newCustomSize() {
            return this.customSize || this.customSizeByPack
        },
    },
    methods: {
    }
}
</script>
