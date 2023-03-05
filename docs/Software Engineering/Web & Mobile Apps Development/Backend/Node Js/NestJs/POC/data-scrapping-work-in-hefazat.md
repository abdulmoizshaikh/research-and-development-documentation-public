# Data scrapping work from price oye in hefazat nestjs backend seed

```jsx showLineNumbers
//model

model ProductMaster {
  productMasterId Int            @id @default(autoincrement())
  category        String
  category2       String?
  category3       String?
  categoryTop     String?
  brand           String
  productModel    String
  source          String?
  sourceProcess   String?
  productTitle    String?
  price           Float?
  categoryGroup   CategoryGroup?
  isMobile        Boolean        @default(false)
  createdAt       DateTime       @default(now())
  createdBy       String         @default("SystemUser")
  updatedAt       DateTime       @updatedAt
  updatedBy       String         @default("SystemUser")
}
```

```jsx showLineNumbers
const priceOyeCategoryMap: any = [
  { group: `B`, category: `Laptops`, poCategory: `laptops`, source: 'priceoye' },
  { group: `B`, category: `Tablets`, poCategory: `tablets`, source: 'priceoye' },
];


private async scrapDataFromPriceOye() {
    for (const entry of priceOyeCategoryMap) {
      await this.scrapProductsDataFromPriceOye(entry.poCategory, entry.category, entry.group, entry.source);
    }
  }

  private async scrapProductsDataFromPriceOye(priceOyeCategory: string, hefazatCategory: string, group: CategoryGroup, source: string) {
    this.logger.log(`Start ${priceOyeCategory} data scrapping from price oye for hefazat category ${hefazatCategory}`);
    try {
      const productListPage = `https://priceoye.pk/${priceOyeCategory}?page=`;
      const productPageListSelector = `#page-category > section.category-sec > div.filter-blist-sec > div.plist-sec > div`;
      let pageNumber = 1;

      const browser = await puppeteer.launch({ executablePath: this.CHROME_PATH, args: ['--no-sandbox'] });
      const page = await browser.newPage();
      let selectorExists = true;
      while (selectorExists) {
        await page.goto(`${productListPage}${pageNumber}`);

        try {
          await page.waitForSelector(productPageListSelector, { timeout: 10000 });
        } catch (e: any) {
          selectorExists = false;
        }
        if (selectorExists) {
          const productLinks = await page.evaluate((productPageListSelector: string) => {
            const anchors = document.querySelectorAll(productPageListSelector).item(0).querySelectorAll('a');
            let links: string[] = [];
            for (const anchor of anchors) {
              const link = anchor.getAttribute(`href`);
              if (link != null && link != ``) {
                links.push(link);
              }
            }
            return links;
          }, productPageListSelector);

          const catgoery = hefazatCategory;
          for (const link of productLinks) {
            const tokens = link.split(`/`);
            let product = tokens[tokens.length - 1];
            product = product.replace(`-`, ` `);
            product = this.common.toTitleCase(product);
            let brand = tokens[tokens.length - 2];
            brand = brand.replace(`-`, ` `);
            brand = this.common.toTitleCase(brand);
            await this.saveProductFromScrapper(catgoery, brand, product, group, source);
          }
        }
        pageNumber += 1;
      }
      await browser.close();
      this.logger.log(`Finishes ${priceOyeCategory} data scrapping from priceoye for hefazat category ${hefazatCategory}`);
    } catch (e: any) {
      this.logger.error(
        `Error while scrapping ${priceOyeCategory} data from priceoye for hefazat category ${hefazatCategory}. ${JSON.stringify(e)}`,
      );
    }
  }

private async saveProductFromScrapper(category: string, brand: string, model: string, group: CategoryGroup, source: string) {
    const existing = await this.prisma.productMaster.findFirst({
      where: {
        category2: category,
        brand: brand,
        productModel: model,
      },
    });
    // price update work
    if (existing == null) {
      await this.prisma.productMaster.create({
        data: {
          brand: brand,
          category: category,
          category2: category,
          productModel: model,
          category3: category,
          categoryGroup: group,
          categoryTop: category,
          isMobile: group == CategoryGroup.C ? true : false,
          productTitle: model,
          source: source,
          sourceProcess: this.SCRAPPER_SOURCE,
          price: 0, //price add
        },
      });
    }
  }
```

**References:**

how to copy selector from chrome inspect element

**How to find CSS selector in Chrome browser**?

Hover the cursor over the image and right click mouse.
Select Inspect.
See the highlighted image code.
Right click on the highlighted code.
Select Copy > Copy selector.

https://amasty.com/knowledge-base/product-labels-find-css-selector.html

How can I get the CSS Selector in Chrome?

```bash showLineNumbers
Right click > Copy > Copy Selector
```

## Reference materials:

**Web scrapping recommended tutorial for JS:**

https://www.youtube.com/watch?v=lgyszZhAZOI&ab_channel=LearnWebCode

Get direct children using querySelectorAll in JavaScript

https://bobbyhadz.com/blog/javascript-queryselectorall-get-direct-children

How to loop through selected elements with document.querySelectorAll

```jsx showLineNumbers
const paragraphs = document.querySelectorAll("p");
paragraphs.forEach((p) => console.log(p));
```

https://stackoverflow.com/questions/12330086/how-to-loop-through-selected-elements-with-document-queryselectorall
