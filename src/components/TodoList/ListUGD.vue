<template>
	<v-main class="list">
		<h3 class="text-h3 font-weight-medium mb-5">Unguided</h3>
        <div class="flex-direction: row">
		<v-card>
			<v-card-title>
				<v-text-field
				v-model="search"
				append-icon="mdi-magnify"
				label="Search"
				single-line
				hide-details
				></v-text-field>
				<v-spacer></v-spacer>
				<v-btn color="success" dark @click="dialog = true">
					Tambah
				</v-btn>	
			</v-card-title>
			<v-data-table :headers="headers" :items="todos" :search="search">
				<template v-slot:[``]="{ }">
					<v-chip >
						
						</v-chip>	
				</template>
				
			</v-data-table>
		</v-card>
        <v-card>
			
               
        </v-card>
        </div>
        
		<v-dialog v-model="dialog" persistent max-width="600px">
 		<v-card>
 			<v-card-title>
 				<span class="headline">Form Todo</span>
 			</v-card-title>
 			<v-card-text>
 				<v-container>
 					<v-text-field
 						v-model="formTodo.task"
 						label="Task"
 						required
 					></v-text-field>

 							<v-select
 								v-model="formTodo.priority"
 								:items="['Penting', 'Biasa', 'Tidak penting']"
								label="Priority"
								required
								
 							></v-select>
				
 					<v-textarea
 						v-model="formTodo.note"
 						label="Note"
 						required
 					></v-textarea>
 				</v-container>
			</v-card-text>
			<v-card-actions>
				<v-spacer></v-spacer>
				<v-btn color="blue darken-1" text @click="cancel">
					Cancel
				</v-btn>
				<v-btn color="blue darken-1" text @click="save">
					Save
				</v-btn>
			</v-card-actions>

		</v-card>
	</v-dialog>
	</v-main>
</template>
<script>
	export default {
		nama: "List",
		data() {
			return {
				search: null,
				dialog: false,
				headers: [
					{
						text: "Task",
						align: "start",
						sortable: true,
						value: "task",	
					},
					
					{ text: "Priority", value: "priority" },
				],
				todos: [
					{
						task: "bernafas",
						priority: "penting",
						note: "huffttt",
					},
					{
						task: "nongkrong",
						priority: "tidak penting",
						note: "bersama teman2",
					},
					{
						task: "masak",
						priority: "biasa",
						note: "masak air 500ml",
					},
				],
				formTodo: {
					task: null,
					priority: null,
					note: null,
				},
			};
		},
		methods: {
			save() {
				this.todos.push(this.formTodo);
				this.resetForm();
				this.dialog = false;
			},
			cancel() {
				this.resetForm();
				this.dialog = false;
			},
			resetForm() {
				this.formTodo = {
					task: null,
					priority: null,
					note: null,
				};
			},
		},
	};
</script>