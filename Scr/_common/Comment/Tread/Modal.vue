<template>
	<app-modal>
		<div class="modal-controls">
			<app-button @click="modal.dismiss()">
				<translate>Close</translate>
			</app-button>
		</div>

		<div class="modal-body">
			<app-comment-widget
				:model="model"
				:thread-comment-id="commentId"
				:show-tabs="false"
				:show-add="false"
				@remove="onRemove"
				@error="onError"
			/>
		</div>

		<div slot="footer" v-if="shouldShowReply">
			<app-message-thread-add
				v-if="parent"
				hide-message-split
				:class="{ '-thread-editor-focus': isEditorFocused }"
			>
				<form-comment
					:comment-model="model"
					:parent-id="parent.id"
					:placeholder="$gettext(`Leave a reply...`)"
					:autofocus="autofocus"
					@submit="_onCommentAdd"
					@editor-focus="onEditorFocus"
					@editor-blur="onEditorBlur"
				/>
			</app-message-thread-add>
		</div>
	</app-modal>
</template>

<style lang="stylus" scoped>
@require '~styles/variables'
// On mobile, we need to make space for the content editor controls. They
// would overlap the Reply form field otherwise.
@media $media-xs
	>>> .message-thread-add.-thread-editor-focus
		padding-bottom: 42px
</style>

<script lang="ts" src="./modal"></script>
