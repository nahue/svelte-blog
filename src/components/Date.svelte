<script>
    import { parseISO, format } from 'date-fns';
    export let date;
    let prettyDate = format(date, 'LLLL	d, yyyy');
    let humanReadableDate = format(date, 'yyyy-MM-dd');
</script>

<time datetime={humanReadableDate}>{prettyDate}</time>
