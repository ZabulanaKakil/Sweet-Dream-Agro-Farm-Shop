# Sweet Dream Agro Farm — Catalog

A one-page catalog for customers. They browse plants, birds and fish, add items to one **Wishlist**, and email it to **tanvir.nahian@dreamersden.org**. Every card shows **Price on request**, plus **Order Now** or **Limited stock**. There is no checkout and no payment on this site.

**Live site:** https://zabulanakakil.github.io/Sweet-Dream-Agro-Farm-Shop/

## Files

| File | What it is |
|------|------------|
| `index.html` | The whole website (layout, style and script in one file) |
| `catalog.csv` | The product list. Open it in Excel. |
| `images/` | Product photos and `logo.jpeg` |

## Change a price, stock or name

1. Download `catalog.csv` from this repo (open the file on GitHub, then the download button).
2. Open it in Excel and edit the cells.
3. **File → Save As → CSV UTF-8 (Comma delimited) (*.csv)**, keep the name `catalog.csv`.
4. On GitHub: **Add file → Upload files**, drop `catalog.csv`, then **Commit changes**.
5. Wait about a minute, then refresh the live site.

Use **CSV UTF-8**. Plain "CSV" can break the taka sign and non-English text.

## Columns in `catalog.csv`

| Column | Meaning |
|--------|---------|
| `code` | Unique product code, such as `OTH03`. Keep it the same when editing a row; customers' saved lists use it. |
| `name` | Name shown on the card |
| `category` | Category chip it appears under. A new name here creates a new chip. |
| `price` | Price in taka, numbers only. `0` or blank shows "Price on request". |
| `sale_price` | Lower promotional price, or blank. Shows a red price and a discount badge. |
| `size` | Short size text, such as `6 inch pot` (optional) |
| `stock` | Number in stock. Used only for the Limited stock tag. It does not block adding to a wishlist. |
| `available` | `yes` for current stock, `no` for inactive / previously sold items. `no` shows **Not available** and **Coming Soon**. |
| `note` | One short description shown when a card is opened (optional) |
| `image` | Photo filename inside `images/`, or blank for a leaf / bird / fish placeholder |

## Add a new product with a photo

1. Name the photo `{category}_{code}_{name}.jpg` in lowercase with hyphens, for example `flower_OTH90_red-rose.jpg`.
2. On GitHub, open the `images` folder, then **Add file → Upload files**, and commit.
3. Add a row to `catalog.csv` with the same filename in the `image` column, and upload the CSV as above.

Keep photos under about 500 KB each so the page loads quickly on mobile data.

## Remove a product

Delete its row from `catalog.csv` and upload the file. The photo can stay in `images/` or be deleted.

## How customer wishlists reach you

When a customer presses **Send wishlist**, their own email app opens with a ready message to tanvir.nahian@dreamersden.org. They press Send there. Subject: `Wishlist from {name}`.

They must fill in:

- Organization or customer name
- Mobile number
- Email
- Delivery method: **Self pickup** or **Deliver to address** (address required if they choose delivery)
- How they found us (required). If they choose “From someone”, they must give that person’s name.

Each mail lists the items and quantities. If they turn on **All in stock**, that line says “all items in stock” instead of a number. Reply to them directly from your inbox.

To change the receiving address, edit `SHOP_EMAIL` near the top of the script in `index.html`, and the address in the footer and Contact section.

## Re-export everything from the shop database

From the PHP shop folder (`websitefiles`), with MySQL running:

```powershell
c:\xampp\php\php.exe database\export_catalog_site.php
```

This rewrites `catalog.csv` and copies the primary photos into `images/` with the naming above. Then commit and push this folder.

## Preview on your computer

Double-clicking `index.html` will not load the catalog, because browsers block reading `catalog.csv` from a local file. Serve the folder instead:

```powershell
c:\xampp\php\php.exe -S 127.0.0.1:8765 -t .
```

Then open http://127.0.0.1:8765/
