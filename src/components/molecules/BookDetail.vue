<template>
  <div class="py-6 mt-5">
    <div
      v-if="book"
      class="lg:grid lg:grid-cols-3 lg:grid-rows-[auto,auto,1fr] lg:gap-x-8"
    >
      <div class="lg:col-span-2 lg:border-r lg:border-gray-200 lg:pr-8">
        <div class="flex">
          <div
            class="hidden w-40 mr-8 bg-gray-200 rounded-md group-hover:opacity-75 sm:block"
          >
            <img
              :src="`https://www.gutenberg.org/cache/epub/${book.id}/pg${book.id}.cover.medium.jpg`"
              alt="Book cover"
              class="object-cover object-center w-full h-full lg:h-full lg:w-full"
            />
          </div>
          <div class="flex flex-col">
            <h1 class="text-2xl font-extrabold tracking-tight text-gray-900">
              {{ book.title }}
            </h1>
            <div class="mt-6">
              <h2 class="text-sm font-medium text-gray-900">Download</h2>
              <div class="mt-6">
                <div class="-my-2 overflow-x-auto">
                  <div class="inline-block min-w-full px-2 py-2 align-middle">
                    <div
                      class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 md:rounded-lg"
                    >
                      <table class="min-w-full divide-y divide-gray-300">
                        <thead class="bg-gray-50">
                          <tr class="divide-x divide-gray-200">
                            <th
                              scope="col"
                              class="px-6 py-4 text-xs font-normal text-left text-gray-900"
                            >
                              Ebook Format
                            </th>
                            <th
                              scope="col"
                              class="px-6 py-4 text-xs font-normal text-left text-gray-900"
                            >
                              Text Format
                            </th>
                          </tr>
                        </thead>
                        <tbody class="bg-white divide-y divide-gray-200">
                          <tr class="divide-x divide-gray-200">
                            <td
                              class="px-6 py-4 text-sm font-medium text-gray-900 whitespace-nowrap"
                            >
                              <a
                                :href="`https://www.gutenberg.org/ebooks/${book.id}.epub.images`"
                                class="text-indigo-600 truncate hover:text-indigo-900"
                              >
                                epub+zip
                              </a>
                            </td>
                            <td
                              class="px-6 py-4 text-sm font-medium text-gray-900 whitespace-nowrap"
                            >
                              <a
                                :href="`https://www.gutenberg.org/ebooks/${book.id}.html.images`"
                                class="text-indigo-600 truncate hover:text-indigo-900"
                              >
                                text/html
                              </a>
                            </td>
                          </tr>
                          <tr class="divide-x divide-gray-200">
                            <td
                              class="px-6 py-4 text-sm font-medium text-gray-900 whitespace-nowrap"
                            >
                              <a
                                :href="`https://www.gutenberg.org/ebooks/${book.id}.kindle.images`"
                                class="text-indigo-600 truncate hover:text-indigo-900"
                              >
                                x-mobipocket-ebook
                              </a>
                            </td>
                            <td
                              class="px-6 py-4 text-sm font-medium text-gray-900 whitespace-nowrap"
                            >
                              <a
                                :href="`https://www.gutenberg.org/file/${book.id}/${book.id}-0.zip`"
                                class="text-indigo-600 truncate hover:text-indigo-900"
                              >
                                text/plain
                              </a>
                            </td>
                          </tr>
                        </tbody>
                      </table>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="mt-6">
          <h3 class="text-sm font-medium text-gray-900">Subjects</h3>
          <div class="mt-3">
            <ul
              v-for="(subject, i) in book.subjects"
              :key="`subject-${i}`"
              role="list"
              class="pl-4 space-y-2 text-sm list-disc"
            >
              <li class="text-gray-400">
                <span class="text-gray-600">{{ subject }}</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <div class="mt-4 lg:row-span-3 lg:mt-0">
        <h2 class="sr-only">Book information</h2>
        <div class="mt-6">
          <h3 class="text-sm font-medium text-gray-900">Total download</h3>
          <div class="mt-3 text-sm text-gray-600">
            {{ book.download_count }}
          </div>
        </div>

        <div class="mt-6">
          <h3 class="text-sm font-medium text-gray-900">Author</h3>
          <div class="mt-3">
            <ul
              v-for="(author, i) in book.authors"
              :key="`author-${i}`"
              role="list"
              class="pl-4 space-y-2 text-sm list-disc"
            >
              <li class="text-gray-400">
                <span class="text-gray-600">{{ author.name }}</span>
                <p class="text-gray-600">
                  {{ author.birth_year }}
                </p>
                <p v-if="author.death_year" class="text-gray-600">
                  {{ "- " + author.death_year }}
                </p>
              </li>
            </ul>
          </div>
        </div>

        <div class="mt-6">
          <h3 class="text-sm font-medium text-gray-900">Bookshelves</h3>
          <div class="mt-3">
            <ul
              v-for="(bookshelve, i) in book.bookshelves"
              :key="`bookshelve-${i}`"
              role="list"
              class="pl-4 space-y-2 text-sm list-disc"
            >
              <li class="text-gray-400">
                <span class="text-gray-600">{{ bookshelve }}</span>
              </li>
            </ul>
          </div>
        </div>

        <div class="mt-6">
          <h3 class="text-sm font-medium text-gray-900">Languages</h3>
          <div class="mt-3">
            <ul
              v-for="(language, i) in book.languages"
              :key="`language-${i}`"
              role="list"
              class="pl-4 space-y-2 text-sm list-disc"
            >
              <li class="text-gray-400">
                <span class="text-gray-600">{{ language }}</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="mt-6">
          <h3 class="mb-2 text-sm font-medium text-gray-900">Gutenberg link</h3>
          <a
            :href="`https://www.gutenberg.org/ebooks/${book.id}`"
            class="mt-3 text-sm text-indigo-600"
          >
            {{ `https://www.gutenberg.org/ebooks/${book.id}` }}
          </a>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    book: {
      type: Object,
      required: true,
      default: () => ({
        id: 84,
        title: "Frankenstein; Or, The Modern Prometheus",
        authors: [
          {
            name: "Shelley, Mary Wollstonecraft",
            birth_year: 1797,
            death_year: 1851
          }
        ],
        translators: [],
        subjects: [
          "Frankenstein's monster (Fictitious character) -- Fiction",
          "Frankenstein, Victor (Fictitious character) -- Fiction",
          "Gothic fiction",
          "Horror tales",
          "Monsters -- Fiction",
          "Science fiction",
          "Scientists -- Fiction"
        ],
        bookshelves: [
          "Gothic Fiction",
          "Movie Books",
          "Precursors of Science Fiction",
          "Science Fiction by Women"
        ],
        languages: ["en"],
        copyright: false,
        media_type: "Text",
        formats: {
          "application/epub+zip":
            "https://www.gutenberg.org/ebooks/84.epub.images",
          "application/rdf+xml": "https://www.gutenberg.org/ebooks/84.rdf",
          "application/x-mobipocket-ebook":
            "https://www.gutenberg.org/ebooks/84.kindle.images",
          "text/html; charset=utf-8":
            "https://www.gutenberg.org/files/84/84-h.zip",
          "text/html": "https://www.gutenberg.org/ebooks/84.html.images",
          "image/jpeg":
            "https://www.gutenberg.org/cache/epub/84/pg84.cover.medium.jpg",
          "text/plain; charset=utf-8":
            "https://www.gutenberg.org/files/84/84-0.zip"
        },
        download_count: 65549
      })
    }
  }
};
</script>
