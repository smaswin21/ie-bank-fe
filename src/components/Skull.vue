<template>
    <div>
        <h1>Skull</h1>
        <p>Environment variables read - file {{ env_var_file_name }}</p>
        <p>{{ msg }}, and it is running from the {{ environment }} environment</p>
        <button type="button" class="btn btn-secondary">
            Skull button
        </button>
    </div>
</template>
 
<script>
import axios from 'axios'
export default
    {
        name: 'Skull',
        data() {
            return {
                msg: `Hi! This is the skull component 💀, running in mode: ${process.env.NODE_ENV} with environment variables defined in ${process.env.VUE_APP_ENV_VAR_FILE_NAME}`
            }
        },
        methods:
        {
            getSkull() {
                const path = `${process.env.VUE_APP_ROOT_URL}/skull`;
                axios.get(path)
                    .then((response) => {
                        this.msg = response.data;
                        this.environment = process.env.NODE_ENV;
                        this.env_var_file_name = process.env.VUE_APP_ENV_VAR_FILE_NAME
                    })
                    .catch(error => console.log(error))
            }
        },
        created() {
            this.getSkull()
        }


    }
</script>
