<template>
  <b-modal
    ok-only
    :ok-disabled="!issue"
    :title="$t('Create or edit an edge model')"
    visible
    @close="toDashboard"
    @ok="startEditing"
  >
    {{ $t('Select the issue that you want to create the edge of.') }}
    <issue-select
      disable-ongoing-or-published
      :disable-not-ongoing-nor-published="false"
      @change="issue = $event && $event.issueNumber ? $event : null"
    />
  </b-modal>
</template>
<script>
import IssueSelect from '@/components/IssueSelect'

export default {
  components: { IssueSelect },
  middleware: ['authenticated', 'is-editor'],
  data() {
    return {
      issue: null,
    }
  },
  methods: {
    toDashboard() {
      window.location.replace(`/`)
    },
    startEditing() {
      window.location.replace(`/edit/${this.issue.publicationCode} ${this.issue.issueNumber}`)
    },
  },
}
</script>
<style></style>
