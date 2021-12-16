<template>
<div>
    <v-dialog
        v-model="dialog"
        max-width="500px"
    >
        <template v-slot:activator="{ on, attrs }">
            <v-btn
                color="primary"
                dark
                v-bind="attrs"
                v-on="on"
            >Add New User</v-btn>
        </template>
        
        <v-card>
            <v-card-title><h5 class="text-h5">Add New User</h5></v-card-title>
            <v-card-text>
                <v-container>
                    <v-row>
                        <v-col cols="12">
                            <v-text-field
                                v-model="name"
                                label="Name"
                                required
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field
                                v-model="job"
                                label="Job"
                                required
                            ></v-text-field>
                        </v-col>
                    </v-row>
                </v-container>
            </v-card-text>
            <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                    color="primary"
                    text
                    @click="dialog = false"
                >Close</v-btn>
                <v-btn
                    color="primary"
                    text
                    @click="addNew(name, job)"
                >Add</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</div>
</template>

<script>
export default {
    name: "addNewDialog",
    data: () => ({
        dialog: false,
        name: "",
        job: "",
    }),
    methods: {
        addNew(name, job){
            const data = {name, job};
            
            fetch('https://reqres.in/api/users', {
                method: 'POST',
                headers: {"Content-Type": "application/json" },
                body: JSON.stringify(data)
            }).then(()=> {
                console.log('new user added');
                this.dialog = false;
            })
        }
    }
}
</script>