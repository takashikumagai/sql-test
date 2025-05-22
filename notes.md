## Practice 1

_RECURSIVE notes_

1. CTE Definition - Anchor Member
    ```
    SELECT
        esec.sales_organization_id AS ancestor_id,
        esec.customer_organization_id AS subordinate_id
    FROM
        enterprise_sales_enterprise_customers AS esec
    ```
    This establishes the direct parent-child relationships.
    This finds all organizations that directly have customers, creating the first level of the hierarchy.

2. CTE Definition - Recursive Member
    ```
    SELECT
        os.ancestor_id,
        esec.customer_organization_id
    FROM
        enterprise_sales_enterprise_customers AS esec
    INNER JOIN
        OrganizationSubordinates AS os
        ON esec.sales_organization_id = os.subordinate_id
    ```
    This finds indirect relationships by joining the current results with the original table, discovering "customers of customers" - if Organization A sells to Organization B, and Organization B sells to Organization C, then C becomes an indirect subordinate of A.

3. The UNION ALL

    The UNION ALL combines the anchor and recursive members, allowing the query to build the complete hierarchy level by level.

## Practice 2

## Practice 3

PostGIS spatial functions

- ST_Contains: true if one contained inside the other
- ST_Intersects: true if one overlaps/touches the other <- use this as the question says _Select japan_segments **within** the bounds_