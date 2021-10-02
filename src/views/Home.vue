<template>
	<div>
		<v-text-field
			clearable
			v-model="newTitle"
			label="Add task..."
			outlined
			append-icon="mdi-plus"
			@click:append="newTask"
			@keyup.enter="newTask"
		></v-text-field>
		<div class="pa-0" v-for="task in tasks" :key="task.id">
			<v-list flat>
				<v-list-item-group v-model="doneTasks" multiple>
					<v-list-item
						@click="doneTask(task.id)"
						:class="{ 'blue lighten-5': task.done }"
					>
						<template v-slot:default>
							<v-list-item-action>
								<v-checkbox
									:input-value="task.done"
									color="primary"
								></v-checkbox>
							</v-list-item-action>

							<v-list-item-content>
								<v-list-item-title
									:class="{
										'text-decoration-line-through grey--text':
											task.done,
									}"
								>
									{{ task.title }}
								</v-list-item-title>
							</v-list-item-content>
							<v-spacer></v-spacer>
							<v-list-item-action @click.stop="delTask(task.id)">
								<v-btn icon>
									<v-icon color="red lighten-2"
										>mdi-trash-can</v-icon
									>
								</v-btn>
							</v-list-item-action>
						</template>
					</v-list-item>
				</v-list-item-group>
			</v-list>
			<v-divider></v-divider>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Home',
	data() {
		return {
			doneTasks: [],
			newTitle: '',
			tasks: [
				{
					id: 1,
					title: 'Something one',
					done: true,
				},
				{
					id: 2,
					title: 'Something number two',
					done: false,
				},
				{
					id: 3,
					title: 'Something number three',
					done: false,
				},
				{
					id: 4,
					title: 'Something number four',
					done: false,
				},
			],
		};
	},
	methods: {
		doneTask(id) {
			let task = this.tasks.filter(t => t.id === id)[0];
			task.done = !task.done;
		},
		delTask(id) {
			this.tasks = this.tasks.filter(t => t.id !== id);
		},
		newTask() {
			if (this.newTitle !== '') {
				let task = {
					id: this.tasks.length + 1,
					title: this.newTitle,
					done: false,
				};
				this.tasks.unshift(task);
				this.newTitle = '';
			}
		},
	},
};
</script>
