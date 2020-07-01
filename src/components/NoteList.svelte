<script>
  import { getContext } from "svelte";
  import { key } from "../context/notes";
  export let notes;
  export let selectedNote;

  const { setSelectedNote } = getContext(key);

  const handleLinkClick = (id) => (event) => {
    event.preventDefault();
    setSelectedNote(id);
  };

  const getTitle = (note) => {
    return note.split(/\n/)[0] || "New note";
  };

  const getBody = (note) => {
    return note.split(/\n/).slice(1).join("");
  };
</script>

<style>
  .note-list {
    border-right: 1px solid var(--border-color);
    height: 100%;
    width: 350px;
  }

  li {
    list-style-type: none;
    border-bottom: 1px solid var(--border-color);
    padding: 1rem;
    margin: 0;
  }

  .title {
    margin: 0;
  }

  .body {
    margin: 0;
  }

  .truncate {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  a.active {
    color: #606c76;
  }
</style>

<section class="note-list">
  <ul>
    {#each notes as note}
      <li class="note-link">
        <a
          href="/"
          class:active={note === selectedNote}
          on:click={handleLinkClick(note.id)}>
          <h5 class="title truncate">{getTitle(note.text)}</h5>
          <p class="body truncate">{getBody(note.text)}</p>
        </a>
      </li>
    {/each}
  </ul>
</section>