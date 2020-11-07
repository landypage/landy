new Vue({
    el: "#{{ include.id }}",
    data: {
        current: {{site.data.site.customers | jsonify }},
        backup: {{site.data.site.customers | jsonify }}
    },
    created(){
        axios.get('{{ site.backend_url }}/site/{{ site.site_id }}/customers', JSON.stringify(this.current))
            .then(response => {
                Object.assign(this.current, response.data);
            })
            .catch(function (error) {
                console.log(error);
            });
    },
    mounted() {
        try {
            $("#{{include.id}}-activate").animatedModal({
                "color": "#ffffff",
                "animatedIn": "slideInDown",
                "animatedOut": "slideOutDown"
            });
        }
        catch(err) {

        }
    },
    methods: {
        close: function () {
            Object.assign(this.current, this.backup);
        },
        save: function () {
            axios.post('{{ site.backend_url }}/site/{{ site.site_id }}/customers', JSON.stringify(this.current))
            .then(function (response) {
                console.log(response);
            })
            .catch(function (error) {
                console.log(error);
            });
        }
    }
});