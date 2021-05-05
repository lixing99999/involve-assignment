<template>
  <div class="p-3 mb-2 bg-lightgrey">
    <div @click="$emit('addRuleGroup')">Rule {{ index + 1 }}</div>
    <div v-for="(rule, idx) in form.rules" :key="idx">
      <div class="d-flex">
        <el-form-item class="m-0">
          <el-select size="mini" v-model="rule.code" placeholder="Select">
            <el-option
              v-for="item in codes"
              :key="item.value"
              :label="item.value"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </el-form-item>

        <el-form-item class="m-0 ml-3">
          <el-select size="mini" v-model="rule.operator" placeholder="Select">
            <el-option
              v-for="item in types"
              :key="item.value"
              :label="item.value"
              :value="item.value"
            >
            </el-option>
          </el-select>
        </el-form-item>

        <el-form-item class="m-0 col">
          <el-input
            size="mini"
            :placeholder="'insert parameter'"
            v-model="rule.value"
          >
            <div
              v-if="idx == 0"
              slot="suffix"
              class="h-100 d-flex align-items-center text-primary font-weight-bold"
              @click="$emit('addRule')"
            >
              add rule
            </div>
            <div
              v-else
              slot="suffix"
              class="h-100 d-flex align-items-center text-danger font-weight-bold"
              @click="$emit('removeRule', { groupIdx: index, idx: idx })"
            >
              remove rule
            </div>
          </el-input>
        </el-form-item>

        <span class="d-flex align-self-center">
          <i
            @click="$emit('removeRuleGroup')"
            :class="idx == 0 ? '' : 'text-dark'"
            class="el-icon-remove-outline text-muted cursor-pointer mr-2 "
            style="font-size:20px"
          />
          <i
            @click="$emit('addRuleGroup')"
            class="el-icon-circle-plus-outline text-dark"
            style="font-size:20px"
          />
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["form", "index"],
  data() {
    return {
      codes: [
        {
          value: "aff_sub"
        }
      ],
      types: [
        {
          value: "is"
        },
        {
          value: "is not"
        }
      ]
    };
  }
};
</script>

<style scoped>
.bg-lightgrey {
  background-color: #eee;
}
</style>
