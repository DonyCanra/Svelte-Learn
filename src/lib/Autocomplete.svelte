<script>
    import { onMount } from 'svelte';

    const items = [
        { name: 'MacBook Air M1', prices: 999, stock: 15 },
        { name: 'MacBook Air M2', prices: 1099, stock: 12 },
        { name: 'MacBook Air M3', prices: 1199, stock: 10 },
        { name: 'MacBook Pro 13" M1', prices: 1299, stock: 8 },
        { name: 'MacBook Pro 14" M1 Pro', prices: 1999, stock: 6 },
        { name: 'MacBook Pro 16" M1 Max', prices: 2999, stock: 4 },
        { name: 'MacBook Pro 13" M2', prices: 1399, stock: 10 },
        { name: 'MacBook Pro 14" M2 Pro', prices: 2099, stock: 7 },
        { name: 'MacBook Pro 16" M2 Max', prices: 3099, stock: 5 },
        { name: 'MacBook Pro 14" M3 Pro', prices: 2199, stock: 8 },
        { name: 'MacBook Pro 16" M3 Max', prices: 3199, stock: 6 },
        { name: 'MacBook Air M1 (16GB RAM)', prices: 1299, stock: 10 },
        { name: 'MacBook Air M2 (16GB RAM)', prices: 1399, stock: 8 },
        { name: 'MacBook Air M3 (16GB RAM)', prices: 1499, stock: 7 },
        { name: 'MacBook Pro 13" M1 (16GB RAM)', prices: 1499, stock: 5 },
        { name: 'MacBook Pro 14" M1 Pro (16GB RAM)', prices: 2199, stock: 4 },
        { name: 'MacBook Pro 16" M1 Max (32GB RAM)', prices: 3499, stock: 3 },
        { name: 'MacBook Pro 13" M2 (16GB RAM)', prices: 1599, stock: 6 },
        { name: 'MacBook Pro 14" M2 Pro (32GB RAM)', prices: 2699, stock: 4 },
        { name: 'MacBook Pro 16" M2 Max (32GB RAM)', prices: 3799, stock: 2 },
        { name: 'MacBook Pro 14" M3 Pro (32GB RAM)', prices: 2899, stock: 5 },
        { name: 'MacBook Pro 16" M3 Max (64GB RAM)', prices: 4299, stock: 3 },
        { name: 'MacBook Air M1 (512GB SSD)', prices: 1199, stock: 12 },
        { name: 'MacBook Air M2 (512GB SSD)', prices: 1299, stock: 10 },
        { name: 'MacBook Air M3 (512GB SSD)', prices: 1399, stock: 8 },
        { name: 'MacBook Pro 13" M1 (512GB SSD)', prices: 1599, stock: 7 },
        { name: 'MacBook Pro 14" M1 Pro (1TB SSD)', prices: 2499, stock: 6 },
        { name: 'MacBook Pro 16" M1 Max (1TB SSD)', prices: 3599, stock: 4 },
        { name: 'MacBook Pro 13" M2 (512GB SSD)', prices: 1699, stock: 8 },
        { name: 'MacBook Pro 14" M2 Pro (1TB SSD)', prices: 2799, stock: 5 },
        { name: 'MacBook Pro 16" M2 Max (2TB SSD)', prices: 4299, stock: 3 },
        { name: 'MacBook Pro 14" M3 Pro (1TB SSD)', prices: 2999, stock: 7 },
        { name: 'MacBook Pro 16" M3 Max (2TB SSD)', prices: 4699, stock: 2 },
        { name: 'MacBook Air M1 (Custom Color)', prices: 1049, stock: 14 },
        { name: 'MacBook Air M2 (Custom Color)', prices: 1149, stock: 12 },
        { name: 'MacBook Air M3 (Custom Color)', prices: 1249, stock: 10 },
        { name: 'MacBook Pro 13" M1 (Custom Color)', prices: 1449, stock: 9 },
        { name: 'MacBook Pro 14" M1 Pro (Custom Color)', prices: 2099, stock: 7 },
        { name: 'MacBook Pro 16" M1 Max (Custom Color)', prices: 3299, stock: 5 },
        { name: 'MacBook Pro 13" M2 (Custom Color)', prices: 1549, stock: 6 },
        { name: 'MacBook Pro 14" M2 Pro (Custom Color)', prices: 2599, stock: 5 },
        { name: 'MacBook Pro 16" M2 Max (Custom Color)', prices: 3999, stock: 3 },
        { name: 'MacBook Pro 14" M3 Pro (Custom Color)', prices: 2799, stock: 6 },
        { name: 'MacBook Pro 16" M3 Max (Custom Color)', prices: 4199, stock: 4 }
    ];

    let query = '';
    let suggestions = [];
    let currentPage = 1;
    const itemsPerPage = 10;

    function updateSuggestions() {
        const lowerCaseQuery = query.toLowerCase();
        suggestions = items.filter(item => 
            item.name.toLowerCase().includes(lowerCaseQuery)
        );
        currentPage = 1; // Reset to first page on new search
    }

    function paginate(items, pageNumber, itemsPerPage) {
        const start = (pageNumber - 1) * itemsPerPage;
        const end = start + itemsPerPage;
        return items.slice(start, end);
    }

    function changePage(pageNumber) {
        currentPage = pageNumber;
    }

    onMount(() => {
        updateSuggestions();
    });
</script>

<main>
    <input 
        type="text" 
        bind:value={query} 
        on:input={updateSuggestions} 
        placeholder="Search for an item..." 
        aria-label="Search for an item"
    />
    <table>
        <thead>
            <tr>
                <th>No.</th>
                <th>Nama Barang</th>
                <th>Price</th>
                <th>Stock</th>
            </tr>
        </thead>
        <tbody>
            {#if suggestions.length > 0}
                {#each paginate(suggestions, currentPage, itemsPerPage) as item, index}
                    <tr>
                        <td>{(currentPage - 1) * itemsPerPage + index + 1}</td>
                        <td>{item.name}</td>
                        <td>{item.prices}</td>
                        <td>{item.stock}</td>
                    </tr>
                {/each}
            {:else}
                <tr>
                    <td colspan="4" style="text-align: center;">Data Tidak Ada</td>
                </tr>
            {/if}
        </tbody>
    </table>
    <div class="pagination">
        {#each Array(Math.ceil(suggestions.length / itemsPerPage)) as _, pageIndex}
            <button 
                on:click={() => changePage(pageIndex + 1)} 
                class:active={currentPage === pageIndex + 1}
            >
                {pageIndex + 1}
            </button>
        {/each}
    </div>
</main>

<style>
    main {
        font-family: Arial, sans-serif;
        padding: 1rem;
    }

    input {
        width: 100%;
        padding: 0.5rem;
        margin-bottom: 1rem;
        border: 1px solid #ccc;
        border-radius: 4px;
        box-sizing: border-box;
    }

    table {
        border-collapse: collapse;
        width: 100%;
    }

    th {
        border: 1px solid #ffffff;
        padding: 0.5rem;
        text-align: left;
    }
    td {
        border: 1px solid #ccc;
        padding: 0.5rem;
        text-align: left;
    }

    th {
        background-color: #00aaff;
    }

    tr:nth-child(even) {
        background-color: #f9f9f9;
        color: black; /* Set text color to black for even rows */
    }

    .pagination {
        margin-top: 1rem;
        text-align: center;
    }

    .pagination button {
        margin: 0 0.25rem;
        padding: 0.5rem 1rem;
        border: 1px solid #ccc;
        background-color: #f9f9f9;
        cursor: pointer;
        color: black;
    }

    .pagination button.active {
        background-color: #00aaff;
        color: white;
    }
</style>