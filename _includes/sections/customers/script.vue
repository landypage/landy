new Vue({
    el: "#{{ include.id }}",
    data: {
        current: {{site.data.site.customers | jsonify }},
        backup: {{site.data.site.customers | jsonify }}
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
        axios
        .get('https://api.coindesk.com/v1/bpi/currentprice.json')
        .then(response => (this.info = response))
    },
    methods: {
        close: function () {
            Object.assign(this.current, this.backup);
        },
        save: function () {
           
        }
    }
});