<template>
    <div style="overflow:hidden;">
        <table class="ivu-table-summary" cellspacing="0" cellpadding="0" border="0" :style="styleObject">
            <colgroup>
                <col v-for="(column, index) in columns" :width="setCellWidth(column)">
            </colgroup>
            <tbody :class="[prefixCls + '-tbody']">
                <tr class="ivu-table-row">
                    <td v-for="(column, index) in columns" :class="alignCls(column)">
                        <div class="ivu-table-cell" :class="cellCls(column)">
                            <span v-if="!data[column.key].render">{{ data[column.key].value }}</span>
                            <render-cell v-else :render="data[column.key].render"></render-cell>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
    import Mixin from './mixin';
    import RenderCell from '../base/render';

    export default {
        name: 'TableSummary',
        components:{
            RenderCell
        },
        mixins: [ Mixin ],
        props: {
            prefixCls: String,
            styleObject: Object,
            columns: Array,
            data: Object,    // rebuildData
            columnsWidth: Object,
            fixed: {
                type: [Boolean, String],
                default: false
            },
        },
        methods: {
            cellCls (column) {
                return [
                    {
                        ['ivu-table-hidden']: (this.fixed === 'left' && column.fixed !== 'left') || (this.fixed === 'right' && column.fixed !== 'right') || (!this.fixed && column.fixed && (column.fixed === 'left' || column.fixed === 'right'))
                    }
                ];
            }
        }
    };
</script>
