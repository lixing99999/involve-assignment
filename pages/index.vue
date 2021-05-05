<template>
  <div>
    <div class="text-center">
      <el-button type="primary" size="medium" @click="showModal = !showModal"
        >Add Revenue Group</el-button
      >
    </div>
    <el-dialog title="Add Revenue Group" :visible.sync="showModal" width="50%">
      <div>
        <el-form ref="form" :model="form">
          <el-form-item label="Revenue Group Title">
            <el-input size="mini" v-model="form.title"></el-input>
          </el-form-item>

          <el-form-item>
            <span class="align-self-center">if </span>
            <el-select size="mini" v-model="form.type" placeholder="Select">
              <el-option
                v-for="item in types"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              >
              </el-option>
            </el-select>
            <span class="align-self-center">
              of the below condition are met</span
            >
          </el-form-item>

          <div>
            <div v-for="(group, idx) in form.ruleGroups" :key="idx">
              <rule-group
                :form="group"
                :index="idx"
                @addRuleGroup="addRuleGroup()"
                @removeRuleGroup="removeRuleGroup(idx)"
                @addRule="addRule(idx)"
                @removeRule="removeRule"
              />
            </div>
          </div>
          <el-form-item class="mt-3">
            <div class="d-flex">
              <span>then revenue is </span>
              <div class="d-flex align-items-center col-md-2">
                <el-input size="mini" v-model="form.revenue" type="number">
                  <div slot="suffix" class="h-100 d-flex align-items-center">
                    %
                  </div>
                </el-input>
              </div>
            </div>
          </el-form-item>
        </el-form>

        <span slot="footer" class="dialog-footer">
          <el-button size="medium" @click="showModal = false">Cancel</el-button>
          <el-button size="medium" type="warning" @click="showModal = false"
            >Confirm</el-button
          >
        </span>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import ruleGroup from "../components/ruleGroup.vue";
export default {
  components: { ruleGroup },
  data() {
    return {
      showModal: true,
      form: {
        title: "",
        type: "",
        revenue: 0,
        ruleGroups: [
          {
            rules: [
              {
                code: "",
                operator: "",
                value: ""
              },
              {
                code: "",
                operator: "",
                value: ""
              }
            ]
          }
        ]
      },
      types: [
        {
          value: "ALL"
        },
        {
          value: "ANY"
        }
      ]
    };
  },
  methods: {
    addRule(idx) {
      this.form.ruleGroups[idx].rules.push({
        code: "",
        operator: "",
        value: ""
      });
    },
    removeRule({ groupIdx, idx }) {
      this.form.ruleGroups[groupIdx].rules.splice(-1, idx);
    },
    addRuleGroup() {
      this.form.ruleGroups.push({
        rules: [
          {
            code: "",
            operator: "",
            value: ""
          }
        ]
      });
    },
    removeRuleGroup(idx) {
      this.form.ruleGroups.splice(-1, idx);
    }
  }
};
</script>
