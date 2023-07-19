  _setData(
            uint256(ETH_NODE),
            address(0),
            uint32(PARENT_CANNOT_CONTROL | CANNOT_UNWRAP),
            MAX_EXPIRY
        );
        _setData(
            uint256(ROOT_NODE),
            address(0),
            uint32(PARENT_CANNOT_CONTROL | CANNOT_UNWRAP),
            MAX_EXPIRY
        );
        names[ROOT_NODE] = "\x00";
        names[ETH_NODE] = "\x03eth\x00";
    }

    function supportsInterface(
        bytes4 interfaceId
    ) public view virtual override(ERC1155Fuse, INameWrapper) returns (bool) {
        return
            interfaceId == type(INameWrapper).interfaceId ||
            interfaceId == type(IERC721Receiver).interfaceId ||
            super.supportsInterface(interfaceId);
    }

    /* ERC1155 Fuse */

    /**
     * @notice Gets the owner of a name
     * @param id Label as a string of the .eth domain to wrap
     * @return owner The owner of the name
     */

    function ownerOf(
        uint256 id
    ) public view override(ERC1155Fuse, INameWrapper) returns (address owner) {
        return super.ownerOf(id);
    }

    /**
     * @notice Gets the owner of a name
     * @param id Namehash of the name
     * @return operator Approved operator of a name
     */

    function getApproved(
        uint256 id
    )
        public
        view
        override(ERC1155Fuse, INameWrapper)
        returns (address operator)
    {
        address owner = ownerOf(id);
        if (owner == address(0)) {
            return address(0);
        }
        return super.getApproved(id);
    }
