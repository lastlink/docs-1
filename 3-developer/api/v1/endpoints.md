# API (v1) Endpoints

**Base API URL: `{{DIRECTUS_ROOT}}/api/1/`**


Resource | Return
:---------|:----------------
**`GET  privileges/:groupId/`**  |  JSON object of the privileges for a given group
**`GET tables/:table/rows/`**  |  Collection of table entries viewable by authenticated user
**`GET tables/:table/rows/:id`**  |  JSON object of a given table entry
**`GET activity/`**  |  Collection of latest directus/db activity
**`GET tables/:table/columns/`**  |  Collection of the column details for a given table
**`GET tables/:table/columns/:column/`**  |  Details for a given column in a given table
**`GET groups/`**  |  Collection of directus user-groups
**`GET groups/:id`**  |  User-group information
**`GET preferences/:table`**  |  Preferences for a given table
**`GET bookmarks/`**  |  Bookmarks for currently authenticated user
**`GET bookmarks/:id`**  |  Bookmark details for a specified bookmark (must belong to authenticated user)
**`GET tables/`**  |  Collection of all tables registered with Directus
**`GET messages/rows`**  |  Collection of messages for the authenticated user
**`GET messages/rows/:id`**  |  Message details for a given message



# Global Parameters

Parameter  |  Example  |  Description
:-----------|:-----------|:-----------------------
**`currentPage`**  |  *`0`, `1`, `2`*  |  Current page for paginated results
**`perPage`**  |  *`100`, `200`, `300`*  |  Number of results per page
**`sort`**  |  *`id`, `title`, `date_uploaded`*  |  Column to sort results upon
**`sort_order`**  |  *`ASC`, `DESC`*  |  Order direction for sorting
**`active`**  |  *`1`, `1,2`, `2`*  |  Filter by a CSV of status values **for tables with a status column** such as `active`
**`columns_visible`**  |  *`title`, `date`*  |  Name of column shown in results. Can be chained such as: `columns_visible=title&columns_visibile=first_name`

