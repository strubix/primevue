<template>
    <DocSectionText v-bind="$attrs">
        <p>Pagination is enabled by adding <i>paginator</i> property and defining <i>rows</i> per page.</p>
    </DocSectionText>
    <DeferredDemo @load="loadDemoData">
        <div class="card">
            <TreeTable :value="nodes" :paginator="true" :rows="5" :rowsPerPageOptions="[5, 10, 25]" tableStyle="min-width: 50rem">
                <Column field="name" header="Name" expander style="width: 34%"></Column>
                <Column field="size" header="Size" style="width: 33%"></Column>
                <Column field="type" header="Type" style="width: 33%"></Column>
                <template #paginatorcontainer="{ first, last, page, pageCount, prevPageCallback, nextPageCallback, totalRecords }">
                    <div class="flex items-center gap-4 border border-primary bg-transparent rounded-full w-full py-1 px-2 justify-between">
                        <Button icon="pi pi-chevron-left" rounded text @click="prevPageCallback" :disabled="page === 0" />
                        <div class="text-color font-medium">
                            <span class="hidden sm:block">Showing {{ first }} to {{ last }} of {{ totalRecords }}</span>
                            <span class="block sm:hidden">Page {{ page + 1 }} of {{ pageCount }}</span>
                        </div>
                        <Button icon="pi pi-chevron-right" rounded text @click="nextPageCallback" :disabled="page === pageCount - 1" />
                    </div>
                </template>
            </TreeTable>
        </div>
    </DeferredDemo>
    <DocSectionCode :code="code" />
</template>

<script>
export default {
    data() {
        return {
            nodes: null,
            code: {
                basic: `
<TreeTable :value="nodes" :paginator="true" :rows="5" :rowsPerPageOptions="[5, 10, 25]" tableStyle="min-width: 50rem">
    <Column field="name" header="Name" expander style="width: 34%"></Column>
    <Column field="size" header="Size" style="width: 33%"></Column>
    <Column field="type" header="Type" style="width: 33%"></Column>
    <template #paginatorcontainer="{ first, last, page, pageCount, prevPageCallback, nextPageCallback, totalRecords }">
        <div class="flex items-center gap-4 border border-primary bg-transparent rounded-full w-full py-1 px-2 justify-between">
            <Button icon="pi pi-chevron-left" rounded text @click="prevPageCallback" :disabled="page === 0" />
            <div class="text-color font-medium">
                <span class="hidden sm:block">Showing {{ first }} to {{ last }} of {{ totalRecords }}</span>
                <span class="block sm:hidden">Page {{ page + 1 }} of {{ pageCount }}</span>
            </div>
            <Button icon="pi pi-chevron-right" rounded text @click="nextPageCallback" :disabled="page === pageCount - 1" />
        </div>
    </template>
</TreeTable>
`,
                options: `
<template>
    <div class="card">
        <TreeTable :value="nodes" :paginator="true" :rows="5" :rowsPerPageOptions="[5, 10, 25]" tableStyle="min-width: 50rem">
            <Column field="name" header="Name" expander style="width: 34%"></Column>
            <Column field="size" header="Size" style="width: 33%"></Column>
            <Column field="type" header="Type" style="width: 33%"></Column>
            <template #paginatorcontainer="{ first, last, page, pageCount, prevPageCallback, nextPageCallback, totalRecords }">
                <div class="flex items-center gap-4 border border-primary bg-transparent rounded-full w-full py-1 px-2 justify-between">
                    <Button icon="pi pi-chevron-left" rounded text @click="prevPageCallback" :disabled="page === 0" />
                    <div class="text-color font-medium">
                        <span class="hidden sm:block">Showing {{ first }} to {{ last }} of {{ totalRecords }}</span>
                        <span class="block sm:hidden">Page {{ page + 1 }} of {{ pageCount }}</span>
                    </div>
                    <Button icon="pi pi-chevron-right" rounded text @click="nextPageCallback" :disabled="page === pageCount - 1" />
                </div>
            </template>
        </TreeTable>
    </div>
</template>

<script>
export default {
    data() {
        return {
            nodes: null,
        }
    },
    created() {
        let files = [];

        for (let i = 0; i < 50; i++) {
            let node = {
                key: i,
                data: {
                    name: 'Item ' + i,
                    size: Math.floor(Math.random() * 1000) + 1 + 'kb',
                    type: 'Type ' + i
                },
                children: [
                    {
                        key: i + ' - 0',
                        data: {
                            name: 'Item ' + i + ' - 0',
                            size: Math.floor(Math.random() * 1000) + 1 + 'kb',
                            type: 'Type ' + i
                        }
                    }
                ]
            };

            files.push(node);
        }

        this.nodes = files;
    }
}
<\/script>
`,
                composition: `
<template>
    <div class="card">
        <TreeTable :value="nodes" :paginator="true" :rows="5" :rowsPerPageOptions="[5, 10, 25]" tableStyle="min-width: 50rem">
            <Column field="name" header="Name" expander style="width: 34%"></Column>
            <Column field="size" header="Size" style="width: 33%"></Column>
            <Column field="type" header="Type" style="width: 33%"></Column>
            <template #paginatorcontainer="{ first, last, page, pageCount, prevPageCallback, nextPageCallback, totalRecords }">
                <div class="flex items-center gap-4 border border-primary bg-transparent rounded-full w-full py-1 px-2 justify-between">
                    <Button icon="pi pi-chevron-left" rounded text @click="prevPageCallback" :disabled="page === 0" />
                    <div class="text-color font-medium">
                        <span class="hidden sm:block">Showing {{ first }} to {{ last }} of {{ totalRecords }}</span>
                        <span class="block sm:hidden">Page {{ page + 1 }} of {{ pageCount }}</span>
                    </div>
                    <Button icon="pi pi-chevron-right" rounded text @click="nextPageCallback" :disabled="page === pageCount - 1" />
                </div>
            </template>
        </TreeTable>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const nodes = ref();

let files = [];
for (let i = 0; i < 50; i++) {
    let node = {
        key: i,
        data: {
            name: 'Item ' + i,
            size: Math.floor(Math.random() * 1000) + 1 + 'kb',
            type: 'Type ' + i
        },
        children: [
            {
                key: i + ' - 0',
                data: {
                    name: 'Item ' + i + ' - 0',
                    size: Math.floor(Math.random() * 1000) + 1 + 'kb',
                    type: 'Type ' + i
                }
            }
        ]
    };

    files.push(node);
}

nodes.value = files;

<\/script>
`
            }
        };
    },
    methods: {
        loadDemoData() {
            let files = [];

            for (let i = 0; i < 50; i++) {
                let node = {
                    key: i,
                    data: {
                        name: 'Item ' + i,
                        size: Math.floor(Math.random() * 1000) + 1 + 'kb',
                        type: 'Type ' + i
                    },
                    children: [
                        {
                            key: i + ' - 0',
                            data: {
                                name: 'Item ' + i + ' - 0',
                                size: Math.floor(Math.random() * 1000) + 1 + 'kb',
                                type: 'Type ' + i
                            }
                        }
                    ]
                };

                files.push(node);
            }

            this.nodes = files;
        }
    }
};
</script>
